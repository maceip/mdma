# Security

`merge-engine` is designed to be a secure, local-only utility for source code management.

## 1. Local Execution
The engine never makes network requests. It does not use external LLM APIs, telemetry, or remote crash reporting. All processing happens on the user's machine, ensuring that proprietary source code never leaves the local environment.

## 2. No Secret Handling
`merge-engine` does not need access to API keys, passwords, or SSH keys. It operates solely on the file contents passed to it by Git or the user.

## 3. Sandboxing (Recommended)
While the engine is written in memory-safe Rust, it parses untrusted source code from different branches. We recommend:
- Running `merge-engine` with the same privileges as your Git client.
- Using standard OS-level permissions to restrict its access to only the repository directory.

## 4. Input Validation
The engine uses Tree-sitter for parsing, which is robust against malformed or malicious source files. If a file fails to parse, the engine safely falls back to line-based merging or emits conflict markers rather than crashing.

## 5. Dependency Management
We strictly limit our dependencies to well-vetted Rust crates:
- `tree-sitter`: For structural analysis.
- `similar`: For textual diffing.
- `thiserror`: For safe error handling.

We use automated CI (GitHub Actions) to scan for vulnerabilities in dependencies.
