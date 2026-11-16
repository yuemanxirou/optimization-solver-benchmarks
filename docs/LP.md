# Linear programming (LP)

LP minimizes or maximizes a linear objective over linear equality and inequality constraints. This page separates **algorithm families** from **solver implementations**: a solver can implement several algorithms.

For a paper-by-paper account of methods, code, and reported effects, see the [LP research map](LP_RESEARCH.md).

> Research status (2026-11-16): Current Mittelmann LP tables have been checked. The inventory is not exhaustive. Performance values are source reports, not independent reproductions.

## Algorithms and implementations

| Family | Main idea | Open implementation / reference | Typical comparison question |
| --- | --- | --- | --- |
| Primal/dual simplex | Move between bases; useful for reoptimization and basis information | [HiGHS](https://github.com/ERGO-Code/HiGHS), [CLP](https://github.com/coin-or/Clp) | How does it perform on sparse LPs and repeated solves? |
| Barrier / interior point | Follow a central path, then optionally crossover to a basis | [HiGHS](https://github.com/ERGO-Code/HiGHS), [Tulip](https://github.com/ds4dm/Tulip.jl) | How do factorization cost and crossover affect wall time? |
| First-order primal-dual | Use inexpensive iterations, often matrix-vector operations | [PDLP in OR-Tools](https://github.com/google/or-tools), [SCS](https://github.com/cvxgrp/scs) | How do scaling and requested accuracy change performance? |
| GPU-oriented first-order | Exploit GPU throughput for large sparse LPs | [cuOpt](https://github.com/NVIDIA/cuopt), [cuPDLPx](https://github.com/MIT-Lu-Lab/cuPDLPx), [HPR-LP-C](https://github.com/PolyU-IOR/HPR-LP-C) | Does data transfer and stopping accuracy offset GPU gains? |

These rows describe broad techniques, not measured superiority. SCS is a conic solver that can accept LPs; a comparison must use the same formulation and stopping criteria.

## Mittelmann results: LPfeas (2026-10-25)

The [source table](https://plato.asu.edu/ftp/lpfeas.html) asks for a primal-dual feasible point on 65 problems. CPU runs used an i7-11700K with 64 GB RAM. The GPU runs used a Xeon Platinum 8570 system with a B200 GPU. The source uses a shifted geometric mean with a 10-second shift, scaled to the best value **within the CPU or GPU group**. The source counts timeout/failure/memory outcomes at its maximum time (15,000 seconds for CPU; 1,000 seconds for GPU). These two hardware groups must not be interpreted as a controlled CPU-vs-GPU speedup.

| CPU solver (source version) | Solved / 65 | Scaled shifted geometric mean |
| --- | ---: | ---: |
| COPT 9.0.0 | 65 | 1.00 |
| MOSEK 11.3.2 | 56 | 3.56 |
| HiGHS 1.15.0 | 55 | 10.2 |
| KNITRO 16.0.0 | 48 | 14.8 |
| PDLP / OR-Tools 9.10 | 50 | 16.6 |
| XOPT 0.0.8 | 59 | 5.77 |

| GPU solver (source version) | Solved / 65 | Scaled shifted geometric mean |
| --- | ---: | ---: |
| cuOpt 26.10 | 62 | 1.37 |
| cuPDLPx 0.3.0 | 57 | 3.55 |
| COPT-H (COPT 9.0.0) | 64 | 1.00 |
| HPR-LP-C 0.1.4 | 63 | 1.34 |

## Mittelmann results: LPopt (2026-10-22)

The [source table](https://plato.asu.edu/ftp/lpopt.html) asks for an **optimal basic solution** on 65 problems, on an i7-11700K with 64 GB RAM. Its shifted geometric mean also uses a 10-second shift, scaled within this table. LPopt and LPfeas test different endpoints; their numbers cannot be merged into one ranking.

| Solver (source version) | Solved / 65 | Scaled shifted geometric mean |
| --- | ---: | ---: |
| CLP 1.17.7 | 40 | 27.4 |
| COPT 9.0.0 | 65 | 1.00 |
| MOSEK 11.2.3 | 53 | 5.27 |
| HiGHS 1.15.0 | 54 | 12.8 |
| GLOP / OR-Tools 9.5 | 33 | 59.7 |
| SoPlex 8.1.0 | 34 | 101 |
| XOPT 0.0.8 | 52 | 6.63 |

## Additional open implementations

| Solver | Algorithm family | Code | Included in the two Mittelmann tables above? |
| --- | --- | --- | --- |
| SCS | First-order conic splitting | [Repository](https://github.com/cvxgrp/scs) | No |
| Tulip | Interior point | [Repository](https://github.com/ds4dm/Tulip.jl) | No |

Do not infer a missing solver's performance from its absence. See the source tables for the exact tested versions of the included solvers.

**Commercial comparison candidates:** Gurobi, CPLEX, and Mosek may appear in benchmark tables. Include them with a clear proprietary license label and official result citation; do not label them open source.

## Mittelmann benchmark tracking

The [Mittelmann benchmark index](https://plato.asu.edu/bench.html) also lists a [large network-LP benchmark](https://plato.asu.edu/ftp/network.html). Its test set is distinct, so it needs its own result table. The index notes that CPLEX, Gurobi, XPRESS, and MindOpt results were removed from its published benchmarks; do not imply their absence is a performance outcome.

## Suggested result format

For each same-condition group, show solved count, total or geometric-mean time as defined by the source, number of failures, and accuracy threshold. Add a performance profile only when per-instance timing data are available. Record whether the time includes presolve, crossover, and GPU transfer. See [benchmark policy](BENCHMARKS.md).

## Follow-up research queue

1. Inspect the current Mittelmann LP pages and identify each participating team, solver, version, and exact test set.
2. Verify recent LP work from those teams using official papers, release notes, and code repositories.
3. Transcribe one dated, same-condition table with a link to every source row.
4. Add a separate table for independent reproductions, if run logs and environment details are available.
