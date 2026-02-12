# Architecture

This document describes the high-level architecture of `merge-engine`.

## Bird's Eye View

`merge-engine` is a non-LLM merge conflict resolver that uses a multi-strategy pipeline to automatically resolve git merge conflicts. It operates as a 3-way merge tool, taking a **base** version and two derived versions (**left** and **right**) to produce a merged result.

The core innovation is a 4-stage pipeline that applies increasingly complex algorithms, stopping as soon as a high-confidence resolution is found.

```
      Conflict Hunk (Base, Left, Right)
               │
               ▼
    ┌───────────────────────┐
    │  1. Pattern Matching  │──► Resolved (High Confidence)
    └───────────────────────┘
               │
               ▼
    ┌───────────────────────┐
    │  2. Structured Merge  │──► Resolved (High Confidence)
    └───────────────────────┘
               │
               ▼
    ┌───────────────────────┐
    │  3. Version Space Alg │──► Ranked Candidates
    └───────────────────────┘
               │
               ▼
    ┌───────────────────────┐
    │  4. Search-based Opt  │──► Ranked Candidates
    └───────────────────────┘
               │
               ▼
      Return Best Candidate or Conflict Markers
```

## The 4-Stage Pipeline

### 1. Pattern-based DSL Rules (`patterns.rs`)
The first stage matches common conflict patterns using a set of domain-specific rules. These include:
- Identical changes on both sides.
- Whitespace-only changes.
- Adjacent edits that don't overlap.
- Import/dependency unions (e.g., adding different imports to the same block).

### 2. Structured Merge (`amalgamator.rs`, `parser.rs`)
Uses **Tree-sitter** to parse the code into Concrete Syntax Trees (CSTs). It performs a tree-level 3-way merge, which can resolve conflicts caused by:
- Code reordering (e.g., two different functions added in different places).
- Formatting changes that confuse line-based diff3.
- Non-overlapping changes to the same syntactic construct.

### 3. Version Space Algebra (`vsa.rs`)
For conflicts that structured merge cannot resolve perfectly, VSA builds a compact representation of the "version space" — all possible ways to combine the edits from Left and Right. It then enumerates and ranks these combinations based on syntactic validity and minimal disruption.

### 4. Search-based Resolution (`search.rs`)
The final fallback uses an evolutionary search (genetic algorithm). It explores the space of potential resolutions, scoring them with a fitness function that measures:
- Token-level similarity to both Left and Right parents.
- Syntactic "shape" preservation.
- Local consistency.

## Codemap

- `main.rs`: CLI interface and Git merge driver wrapper.
- `lib.rs`: Library entry point and public API.
- `resolver.rs`: The orchestrator that manages the 4-stage pipeline.
- `types.rs`: Core types: `CstNode`, `MergeScenario`, `ResolutionCandidate`.
- `parser.rs`: Tree-sitter integration for multiple languages.
- `diff3.rs`: Internal implementation of the standard 3-way text merge used for hunk extraction.
- `matcher.rs`: Tree-matching algorithms used to align CST nodes between versions.

## Invariants

- **Safety First:** If the engine cannot find a resolution with sufficient confidence, it must emit standard Git conflict markers rather than a "best guess" that might break the build.
- **Language Agnostic (mostly):** While structured merge requires a Tree-sitter grammar, the Pattern and Search stages are designed to be largely language-agnostic.
- **Local Only:** No network calls or LLMs are used, ensuring privacy and speed.

## Supported Languages

The engine uses Tree-sitter for structured merge and VSA. Currently supported:
- Rust, JavaScript, TypeScript, Python, Java, Go, C, C++, Kotlin, TOML, YAML.
