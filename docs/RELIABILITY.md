# Reliability & Robustness

`merge-engine` is designed to be a "fail-safe" tool. If it cannot guarantee a correct merge, it must not corrupt the source code.

## 1. Fallback Chain
Reliability is achieved through a strict hierarchy of fallbacks:
1. **Rule Failure:** If a DSL rule doesn't match perfectly, it's skipped.
2. **Parse Failure:** If Tree-sitter cannot parse a file (e.g., due to syntax errors in a conflict), the structured merge stage is skipped.
3. **Synthesis Failure:** If VSA or Search cannot find a candidate with a high enough confidence score, the engine defaults to standard Git conflict markers.

## 2. Syntactic Validation
Resolutions produced by the VSA and Search stages are optionally passed back through the parser to ensure they are at least syntactically valid before being presented to the user.

## 3. Preservation of Intent
A key reliability metric is whether the engine preserves the "intent" of both the Left and Right branches. Our fitness functions are biased towards:
- Minimizing deleted tokens that were present in either parent but not the other.
- Maximizing the preservation of syntactic blocks.

## 4. Error Handling
We use the `anyhow` and `thiserror` crates to ensure that errors (file I/O, parsing, timeouts) are caught and handled gracefully. A crash in the merge engine should never leave a repository in an inconsistent state.

## 5. Test Coverage
- **Unit Tests:** Every module (`vsa`, `matcher`, `amalgamator`) has >80% test coverage.
- **Property-based Testing:** We use `proptest` (planned) to ensure that the merge engine is stable across a wide range of synthetic conflict scenarios.
- **Integration Tests:** The `ground_truth` suite ensures no regressions on known hard conflicts.
