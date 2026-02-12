# merge-engine Knowledge Base — Table of Contents

This file serves as the entry point for understanding the `merge-engine` project. It provides pointers to detailed documentation covering architecture, design decisions, and project planning.

## ExecPlans

When writing complex features or significant refactors, use an ExecPlan (as described in [docs/PLANS.md](docs/PLANS.md)) from design to implementation.

## Architecture & Code

| Document | What it covers |
|----------|---------------|
| [ARCHITECTURE.md](ARCHITECTURE.md) | High-level system design, the 4-stage resolution pipeline, and crate structure. |
| [docs/DESIGN.md](docs/DESIGN.md) | Design philosophy, academic foundations (VSA, Structured Merge), and strategy selection. |
| [docs/QUALITY_SCORE.md](docs/QUALITY_SCORE.md) | How we measure resolution accuracy, confidence levels, and benchmarking against ground truth. |
| [docs/SECURITY.md](docs/SECURITY.md) | Security model for a local-only development tool. |
| [docs/RELIABILITY.md](docs/RELIABILITY.md) | Error handling, parsing fallback strategies, and pipeline robustness. |

## Product & Planning

| Document | What it covers |
|----------|---------------|
| [docs/PLANS.md](docs/PLANS.md) | Roadmap, language support expansion, and performance optimizations. |
| [docs/PRODUCT_SENSE.md](docs/PRODUCT_SENSE.md) | Target use cases (Git merge driver, IDE integration) and core value proposition. |
| [docs/exec-plans/](docs/exec-plans/) | Active and completed execution plans for specific features. |
| [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) | Common issues with tree-sitter parsing and git integration. |

## Maintenance

The documentation and code quality are maintained through automated checks:

- **`.github/workflows/ci.yml`** — Runs `cargo test`, `clippy`, and `fmt` on every push.
- **`tests/ground_truth.rs`** — Integration tests against known complex merge scenarios.
