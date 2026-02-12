# Quality & Benchmarking

We measure the quality of `merge-engine` across three primary metrics: **Accuracy**, **Recall**, and **Performance**.

## 1. Resolution Accuracy (Confidence)
Every resolution produced by the engine is assigned a `Confidence` score:
- **High:** Pattern matches or clean structured merge. The code is almost certainly correct.
- **Medium:** VSA produced a candidate that is syntactically valid and has high similarity to both parents.
- **Low:** Search-based resolution fallback. Requires human review.

## 2. Recall (Auto-Resolution Rate)
This is the percentage of conflicts that the engine can resolve without human intervention. We benchmark this against the `tests/ground_truth.rs` suite, which contains real-world conflicts from large open-source repositories.

| Project Type | diff3 (Git) | merge-engine (Target) |
|--------------|-------------|-----------------------|
| Rust / Cargo | 0% (Baseline)| 85%                   |
| TypeScript   | 0% (Baseline)| 80%                   |
| Python       | 0% (Baseline)| 90%                   |

## 3. Performance SLOs
Merge resolution should be fast enough to be invisible in a developer's workflow.

| Metric | Target |
|--------|--------|
| Startup Time | < 10ms |
| Conflict Resolution (Rule/Structured) | < 50ms |
| Conflict Resolution (Search-based) | < 500ms |
| Memory Usage | < 100MB |

## Benchmarking Suite
We maintain a "ground truth" dataset in `tests/data/`. This includes:
- **Base/Left/Right triplets:** The input to the merge.
- **Expected Resolution:** The manually verified "correct" merge result.
- **Metadata:** Why the conflict happened (e.g., "reordered imports").

Run benchmarks with:
```bash
cargo test --test ground_truth -- --ignored
```
