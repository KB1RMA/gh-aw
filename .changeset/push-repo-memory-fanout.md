---
"gh-aw": patch
---

Stop serializing the `push_repo_memory` job through a shared concurrency group. GitHub Actions keeps only one pending job per group and cancels the rest, so when many runs finished at once all but two pushes to a repo-memory branch were cancelled and their memory silently lost. Concurrent pushes now converge through the existing compare-and-swap push with up to 10 jittered, capped retries.
