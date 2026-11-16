# Optimization Algorithms & Benchmarks

An evidence-first catalog of algorithms and solvers for LP, QP, QCQP, SOCP, SDP, NLP, and MIP. The first populated section is [linear programming](docs/LP.md), with a [paper-level research map](docs/LP_RESEARCH.md).

> Status (2026-11-16): Mittelmann's LPfeas (2026-10-25) and LPopt (2026-10-22) tables were checked. Values below are benchmark-maintainer reports, not our own reproductions.

## Browse by problem class

| Class | Model | Catalog |
| --- | --- | --- |
| LP | Linear objective and linear constraints | [LP](docs/LP.md) |
| QP | Quadratic objective and linear constraints | Planned |
| QCQP | Quadratic objective and quadratic constraints | Planned |
| SOCP | Linear objective and second-order cone constraints | Planned |
| SDP | Semidefinite cone constraints | Planned |
| NLP | General nonlinear objective or constraints | Planned |
| MIP | Integrality constraints | Planned |

## How results are compared

Only results from the **same benchmark suite, instance set, hardware class, thread count, time limit, feasibility/optimality tolerances, and solver versions** belong in one performance table. A missing result is `—`, never a zero. We distinguish an author's reported result from an independently reproduced result. See [benchmark policy](docs/BENCHMARKS.md).

### LP comparison panel

| Source / suite | Task | Best reported solved count | Best reported scaled shifted geometric mean |
| --- | --- | --- | --- |
| [LPfeas, 2026-10-25](https://plato.asu.edu/ftp/lpfeas.html) | Find a primal-dual feasible point | COPT 65/65 (CPU); COPT-H 64/65 (GPU) | COPT 1.00 (CPU); COPT-H 1.00 (GPU) |
| [LPopt, 2026-10-22](https://plato.asu.edu/ftp/lpopt.html) | Find an optimal basic solution | COPT 65/65 | COPT 1.00 |

The metric is scaled **within each table**, so its 1.00 values cannot be compared across LPfeas and LPopt. LPfeas CPU and GPU runs also used different hardware and time limits; their columns are separate. See [all reported solver results](docs/LP.md).

For individual papers, implementations, and author-reported effects, see the [LP research map](docs/LP_RESEARCH.md). It includes the PDLP, cuPDLP, HPR-LP, presolve, scaling, crossover, infeasibility, and distributed-GPU lines of work. Paper experiments and Mittelmann's later solver versions are kept separate.

## Existing resources

Related work already exists: [Awesome Operations Research](https://github.com/SirMore/Awesome-Operations-Research/blob/main/solver-comparison.md) compares solver coverage and licensing; [solver_benchmarks](https://github.com/bodono/solver_benchmarks) provides a benchmark harness; [Mittelmann's benchmark index](https://plato.asu.edu/bench.html) publishes results across problem classes. This project focuses on source-linked algorithm and solver entries with same-condition result tables. We do not claim to be the first optimization catalog.

## Contribute

Add an entry with an official paper or documentation link, code/license link where applicable, and a precise result citation. Use the fields in [the contribution guide](CONTRIBUTING.md). Do not compare numbers across different test conditions.

## License

MIT; see [LICENSE](LICENSE). Upstream papers, code, and benchmark data retain their own licenses.
