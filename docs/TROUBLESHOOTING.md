# Troubleshooting

Common issues when using `merge-engine`.

## 1. Tree-sitter Parsing Errors
If you see "Failed to parse" errors, it usually means the source file contains syntax that the current Tree-sitter grammar doesn't recognize.
- **Solution:** Ensure your code is syntactically valid before merging. If the language is new, check if the corresponding `tree-sitter-*` crate is enabled in `Cargo.toml`.

## 2. Git Driver Not Working
If git is not using `merge-engine` for conflicts:
- **Check `.gitconfig`:** Ensure the `[merge "merge-engine"]` section is correct and the `driver` path is in your `PATH`.
- **Check `.gitattributes`:** Ensure the file extensions you want to merge are mapped to the `merge-engine` driver (e.g., `*.rs merge=merge-engine`).

## 3. Unexpected Conflict Markers
If the engine fails to resolve a conflict and emits markers:
- **Explanation:** This is the default safety behavior when confidence is low.
- **Debug:** Run `merge-engine` manually on the conflict files with the `--debug` flag to see which strategies were tried and why they failed.

## 4. Performance Issues on Large Files
Structured merge can be memory-intensive for extremely large files.
- **Solution:** If a file is too large, `merge-engine` will attempt to fall back to `diff3`. You can tune the `max_vsa_candidates` in `ResolverConfig` to speed up the VSA stage.

## 5. Encoding Problems
`merge-engine` expects UTF-8 encoded files.
- **Solution:** Convert non-UTF-8 files before merging. Support for other encodings is planned but not currently a priority.
