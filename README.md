# GERB: Graduate Economic Reasoning Benchmark

GERB tests whether a red herring corrupts a language model's economic reasoning. A red herring is text added to
the problem that looks relevant to it but is not needed to solve it, and it leaves the verified answer and
the operative mechanism unchanged. The benchmark is built on
sixty graduate-level microeconomics problems, each with one objectively verifiable answer and a full
step-by-step reference solution. Every problem is fielded in a 2x2 within-task design that crosses the red
herring with a request for the model to explain itself. Because the manipulation is within task, the red
herring is orthogonal to task difficulty by construction, and its effect is identified against model and task
fixed effects rather than measured as a raw accuracy drop.

The loss the paper measures comes from distraction, not from added text. A common red herring, the same text
in every task, leaves the answer unchanged by the same verified standard, is plausible for no task, and does
nothing. The damage is confined to tailored red herrings that make a plausible but incorrect argument for the
task's own answer, and whether a model is derailed by one is a property of the model, not of the prompt.

GERB follows a **public design, private content** model. The design, the grading rules, the grade ruling, the
analysis code and the full results are open. The problem statements and reference solutions are held
privately so the benchmark stays out of training corpora, and are released only under a data-use agreement.
See [DATA_ACCESS.md](DATA_ACCESS.md).

GERB shares its sixty-problem corpus with **GEMB**, the Graduate Economic Metacognition Benchmark, which
applies a different protocol to the same problems. The two benchmarks differ in what they measure, not in the
underlying problems.

## What is in this repository (public)

| Path | Contents |
|------|----------|
| [PROTOCOL.md](PROTOCOL.md) | The experimental design, the two-stage grading, the grade ruling and the estimand |
| `results/` | The outcome tables and per-model estimates reported in the paper, under the ruled grade, on the paper's fifty-nine-task estimation sample; `results/README.md` states the step from the sixty problems to the fifty-nine |
| `examples/` | A small number of illustrative problems, enough to convey the style |
| [CITATION.cff](CITATION.cff), [CITATION.bib](CITATION.bib) | How to cite GERB |
| [DATA_ACCESS.md](DATA_ACCESS.md) | How to request the private problem set, and the terms |

## What is not in this repository (private, on request)

The sixty problem statements and their reference solutions, the models' response texts and final-answer
strings, and the grade-ruling code, which encodes the verified answers of the tasks it regrades. Releasing
the problems publicly would let them leak into the next training run and destroy the benchmark's resistance
to contamination, so they are served only under the agreement in [DATA_ACCESS.md](DATA_ACCESS.md). The
benchmark is fully reproducible in method from this repository. The paper's full replication materials, the data
and the analysis code, are distributed with the paper, not in this benchmark repository, and scoring a new model
on GERB needs the private problems.

## Summary of the study

Thirty-eight language models answered all four versions of all sixty problems, five times each, in independent
stateless calls at temperature zero. Grading is two-stage, a deterministic rule for terse, unambiguous answers
and an independent judge model for everything else, with a second judge regrading a subsample. A deterministic
grade ruling corrects the grader's verdicts before any estimate. Of the sixty problems, fifty-nine carry a
passage that leaves every assumption and the final answer unchanged, and these fifty-nine are the estimation
sample. On it the red herring lowers the probability of a correct answer by about fourteen percentage points.
The effect does not differ between models that reason by default and models that do not, and it is largest on
the problems a model rates as easy. Neutral content does not lower accuracy. The common red herring and the
tailored red herrings that do not argue a wrong answer have an effect indistinguishable from zero, and the
plausible but incorrect arguments account for essentially all of the loss. Full results are in the paper and
in `results/`.

## How to cite

Cite the paper and the archived release. Ready-to-use entries are in [CITATION.bib](CITATION.bib). This is
version 3.0.0 of the release (2026-10-22), the benchmark under the ruled grade.

## License

The materials in this repository are released under CC BY 4.0, except the code, which is released under the
MIT license in [LICENSE-CODE.txt](LICENSE-CODE.txt). The private problem set is not covered by either license
and is governed solely by the data-use agreement in [DATA_ACCESS.md](DATA_ACCESS.md).

## Contact

Piyush Akimitsu, Department of Economics, University at Albany, SUNY. The contact address for access requests
is in [DATA_ACCESS.md](DATA_ACCESS.md).
