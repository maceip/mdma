# Tech Debt Tracker

This document tracks known technical debt and architectural gaps in `merge-engine`.

## Active Debt

| ID | Priority | Area | Description | Status |
|----|----------|------|-------------|--------|
| TD1 | P1 | Testing | No property-based testing for VSA and Search strategies. | Open |
| TD2 | P1 | Parsing | Tree-sitter errors are reported as generic strings; need structured error types. | Open |
| TD3 | P2 | Performance | `amalgamator` matching algorithm is O(N^2); needs optimization for large trees. | Open |
| TD4 | P2 | CLI | Manual argument parsing in `main.rs` is becoming brittle. | Open |
| TD5 | P2 | Patterns | Heuristics for "adjacent edits" in `patterns.rs` are too conservative. | Open |
| TD6 | P3 | Refactoring | `types.rs` is monolithic; should be split into `ast`, `merge`, and `config`. | Open |

## Process

1. **Discovery:** When you encounter code that is hard to maintain or deviates from our design principles, add it here.
2. **Resolution:** When debt is paid down, remove the entry and record the outcome in the relevant ExecPlan.
3. **Review:** Prioritize P1 items in the next `PLANS.md` roadmap update.
