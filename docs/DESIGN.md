# Design Philosophy

`merge-engine` is built on several core technical beliefs about the future of developer tools and program analysis.

## 1. Non-LLM Priority
While LLMs are powerful, merge conflict resolution is often a deterministic or semi-deterministic task that benefits from the speed, cost-efficiency, and 100% reproducibility of symbolic and search-based methods. We prioritize "classical" program analysis techniques (CST merging, VSA) because they provide explainable and verifiable results.

## 2. Confidence-Driven Pipeline
Not all resolutions are created equal. Our architecture is designed as a "cascade" where the fastest and most reliable methods run first.
- **Rules** are 100% confident.
- **Structured Merge** is ~95% confident (syntactically).
- **VSA and Search** provide a ranked list of candidates with varying confidence scores.

## 3. Structural over Textual
Line-based merging (like standard `git merge`) is a relic of an era when tools didn't understand code structure. By lifting the merge process from lines of text to Concrete Syntax Trees, we eliminate a huge class of "false" conflicts caused by reformatting, comment changes, or non-conflicting syntactic edits.

## 4. Academic Foundations
The strategies implemented in `merge-engine` are based on peer-reviewed research:
- **DSL Patterns:** Based on Svyatkovskiy et al. (ICSE 2021).
- **Structured Merge:** Inspired by LASTMERGE (2025) and AutoMerge.
- **VSA:** Based on Version Space Algebra for program synthesis (OOPSLA 2018).
- **Search-Based:** Based on token-similarity fitness functions (TOSEM 2025).

## 5. Local and Fast
A merge tool should not require an internet connection or an expensive GPU. `merge-engine` is written in Rust for maximum performance and is designed to run in milliseconds as part of a standard `git merge` or `git pull` workflow.
