# Git Integration UX Improvement

This ExecPlan is a living document. The sections `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes & Retrospective` must be kept up to date as work proceeds.

This document is maintained in accordance with `/docs/PLANS.md`.

## Purpose / Big Picture

The goal of this task is to improve the usability of `merge-engine` when used as a git merge driver or standalone tool. Currently, the CLI has inconsistent flag handling and basic conflict marker parsing. We want to:
1. Standardize CLI flags (e.g., `--version`, `--help`, `-v`).
2. Improve `resolve_stdin` to handle nested or malformed markers gracefully.
3. Ensure the git merge driver mode accurately reports success/failure to git via exit codes.

## Progress

- [ ] (2026-02-12 22:45Z) Standardize CLI flags and add `--version`.
- [ ] (2026-02-12 22:45Z) Refactor `parse_conflict_markers` for better robustness.
- [ ] (2026-02-12 22:45Z) Add integration tests for CLI usage.

## Surprises & Discoveries

- (None yet)

## Decision Log

- Decision: Use `clap` or a similar crate for argument parsing? 
  Rationale: To keep dependencies minimal and binary size small, we will stick to manual parsing for now unless it becomes too complex.
  Date/Author: 2026-02-12 / Agent

## Outcomes & Retrospective

- (To be filled on completion)

## Context and Orientation

- `src/main.rs`: Contains the CLI logic and `resolve_stdin` implementation.
- `src/resolver.rs`: The core logic called by the CLI.

## Plan of Work

1. **CLI Refactoring:** Update `main` in `src/main.rs` to support `-V`, `--version`, `-h`, `--help`. Use a more structured approach to parsing positional arguments.
2. **Conflict Marker Parsing:** Enhance `parse_conflict_markers` in `src/main.rs` to handle cases where `||||||| BASE` is missing (some git configs don't include it).
3. **Exit Codes:** Ensure that in git driver mode, returning `1` correctly signals git that conflicts remain, while `0` signals a clean merge.

## Concrete Steps

1. Edit `src/main.rs` to add version/help handling.
2. Run `cargo build`.
3. Test with `merge-engine --version`.

## Validation and Acceptance

- `merge-engine --version` prints the correct version from `Cargo.toml`.
- Running `merge-engine --stdin` on a file with diff2 markers (no BASE) still resolves correctly if possible.
- Exit code is `0` for fully resolved merges and `1` for partial/failed merges.
