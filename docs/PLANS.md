# merge-engine Execution Plans (ExecPlans)

This document describes the requirements for an execution plan ("ExecPlan"), a design document that a coding agent can follow to deliver a working feature or system change. Treat the reader as a complete beginner to this repository: they have only the current working tree and the single ExecPlan file you provide. There is no memory of prior plans and no external context.

## How to use ExecPlans and PLANS.md

When authoring an executable specification (ExecPlan), follow this document _to the letter_. Be thorough in reading (and re-reading) source material to produce an accurate specification. When creating a spec, start from the skeleton and flesh it out as you do your research.

When implementing an executable specification (ExecPlan), do not prompt the user for "next steps"; simply proceed to the next milestone. Keep all sections up to date, add or split entries in the list at every stopping point to affirmatively state the progress made and next steps. Resolve ambiguities autonomously, and commit frequently.

When discussing an executable specification (ExecPlan), record decisions in a log in the spec for posterity. ExecPlans are living documents, and it should always be possible to restart from _only_ the ExecPlan and no other work.

## Requirements

- **Fully Self-Contained:** Every ExecPlan must contain all knowledge and instructions needed for a novice to succeed.
- **Living Document:** Revise it as progress is made. Each revision must remain fully self-contained.
- **Outcome-Focused:** Every ExecPlan must produce a demonstrably working behavior.
- **Plain Language:** Define every term of art or technical jargon immediately.

## Skeleton of a Good ExecPlan

```md
# <Short, action-oriented description>

This ExecPlan is a living document. The sections `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes & Retrospective` must be kept up to date as work proceeds.

This document must be maintained in accordance with /docs/PLANS.md.

## Purpose / Big Picture

Explain in a few sentences what someone gains after this change and how they can see it working.

## Progress

- [ ] (YYYY-MM-DD HH:MMZ) Task description.

## Surprises & Discoveries

Document unexpected behaviors, bugs, or insights.

## Decision Log

- Decision: ...
  Rationale: ...
  Date/Author: ...

## Outcomes & Retrospective

Summarize outcomes, gaps, and lessons learned at completion.

## Context and Orientation

Describe the current state relevant to this task. Name the key files and modules by full path.

## Plan of Work

Describe, in prose, the sequence of edits and additions.

## Concrete Steps

State the exact commands to run and where to run them.

## Validation and Acceptance

Describe how to start or exercise the system and what to observe.
```

## Roadmap

### Current Focus
- [ ] **Git Integration UX:** Standardize CLI flags and improve conflict marker parsing.
- [ ] **Language Coverage:** Add support for C# and Swift.
- [ ] **Performance:** Benchmarking and optimizing VSA candidate generation.

### Near-term
- **Interactive Mode:** A TUI for choosing between ranked candidates.
- **Custom DSL:** Configurable pattern rules.
