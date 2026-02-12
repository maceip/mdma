# Product Sense

## Who is `merge-engine` for?

**Primary user:** Software engineers and DevOps teams who want to automate the resolution of git merge conflicts without relying on slow, non-deterministic, or privacy-invasive LLMs.

**Jobs to be done:**

1. **Reduce "Merge Hell":** Automatically resolve the 80-90% of conflicts that are syntactically trivial but line-conflicting.
2. **Improve Productivity:** Spend less time manually clicking "Accept Left" or "Accept Right" in an IDE for repetitive conflicts like import reordering.
3. **Safe Automation:** Confidently use the tool in CI/CD pipelines to auto-merge branches that would otherwise require manual intervention.
4. **Local Privacy:** Resolve conflicts on proprietary codebases without sending data to third-party AI providers.

## Product Principles

1. **Safety is Paramount:** A false resolution is much worse than no resolution. We prefer falling back to conflict markers over producing broken code.
2. **Deterministic by Default:** Rule-based and structured merge strategies are deterministic, ensuring consistent behavior across different environments.
3. **Seamless Integration:** Works as a drop-in replacement for standard git merge drivers.
4. **Performance as a Feature:** The tool must be fast enough to run as a git hook without noticeable delay.

## Non-goals

- Replacing human code review for semantic conflicts (e.g., two people changing the logic of the same algorithm in incompatible ways).
- Being a full-featured IDE (we focus on the merge engine, not the UI).
- Competing with general-purpose AI assistants (we are a specialized tool for structural merging).
