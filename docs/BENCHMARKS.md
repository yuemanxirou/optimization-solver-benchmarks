# Benchmark policy

## Required provenance for every result

- Original table or paper URL and access/publication date
- Problem class and exact test suite, including excluded instances
- Solver name, version or commit, algorithm mode, and license class
- Hardware, operating system, CPU/GPU, memory, and thread count
- Time limit, numerical tolerances, presolve/scaling/crossover settings
- Metric definition (including treatment of failures and timeouts)
- Whether the result is author-reported, benchmark-maintainer-reported, or independently reproduced

## Comparability rule

Group results only when all test conditions above agree. Where the source omits a condition, mark it unknown and avoid a ranking. Never convert a published geometric mean into an arithmetic mean. Never combine a GPU wall time with a CPU time without stating transfer and setup accounting.

## Updating a snapshot

Each snapshot should live in `data/<problem-class>/<source>-<YYYY-MM-DD>.csv` with a neighboring `.md` file that records provenance and exact column meanings. Preserve old snapshots so changes in solver versions or suites remain visible.
