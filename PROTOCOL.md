# GERB protocol

This document specifies the design precisely enough to reproduce the benchmark in method. The sixty problems
and their reference solutions are the private component and are described here only structurally.

## The corpus

Sixty microeconomics problems written at graduate level. They span consumer choice, labor supply and time
allocation, household production, monopoly and Cournot competition, production and factor demand,
externalities and bargaining, price ceilings and floors, demand and supply elasticity, signaling and
screening, and competitive equilibrium. Each problem states a structured multi-part setup, with named blocks
for the environment, the budget or constraint, and the cost or payoff structure. Statements run a median of
226 words. Each problem has exactly one objectively verifiable answer, of one of four types, numeric,
number-tuple, categorical or symbolic. Each carries a full step-by-step reference solution whose intermediate
quantities can be checked one by one. In their released form the problems appear in no public benchmark and
no indexable public source.

## The 2x2 within-task design

Two factors are manipulated inside every problem.

- **Red herring, d in {0, 1}.** Text added to the problem. It looks relevant to the problem, is not needed to
  solve it, and leaves the verified answer, the reference solution and the operative mechanism unchanged. The treatment and control versions of a problem therefore share the same
  answer and the same reference solution. The red herring adds a median of 37 words.
- **Explanation request, e in {0, 1}.** The explain version appends the verbatim sentence "Provide a complete
  explanation." The no-explain version appends nothing.

Crossing the two factors gives four versions of every problem, 240 versions in all.

## Administration

Each contestant model answers all 240 versions in five waves, at temperature zero, in independent single-turn
calls with no shared state and no reasoning parameter set, so every model runs in its default deployed mode.
Models are reached through a gateway in their default deployed configuration. In the reference study this is
60 x 4 x 38 x 5 = 45,600 planned responses.

## The estimation sample

Of the sixty problems, fifty-nine carry a passage that leaves every assumption and the final answer unchanged,
and these fifty-nine are the estimation sample used everywhere in the paper. The sixtieth carries a red herring
that changes its answer, so it fails the screen that defines a valid red herring and falls outside the sample.

## Grading

Grading is two-stage. The first stage covers no-explanation responses whose answer is terse and unambiguous,
a single number or a short categorical word or phrase. A deterministic rule compares the answer with the
verified answer, to within rounding for a number, and assigns final-answer correctness directly with no judge
call. In the second stage, every other response is graded by an independent judge model in its own
conversation after the contestant has finished. That covers all explanation-requested versions and any
no-explanation answer that is long, a formula, or otherwise ambiguous. The contestant never sees the verified
answer or the worked solution. Only the judge does.

On explanation-requested versions the judge returns four binary marks.

1. **Answer correct.** The final answer matches the verified answer.
2. **Explanation given.** The response contains an explanation.
3. **Reasoning correct.** The reasoning shown is equivalent to the reference solution.
4. **Coherent.** The answer follows from the reasoning shown.

On no-explanation versions the answer-correct mark is graded for every response, and whether an explanation
was given is graded for every response in a second pass, since a model can explain without being asked.
Reasoning-correct and coherence are defined only where an explanation exists. On the explanation-requested
arm, a response that returns no explanation is coded zero on the reasoning mark rather than left ungraded.
On the no-explanation arm the two marks are computed only over the responses that explained unprompted and are
not reported as condition means.

To bound dependence on the judge, a second independent judge regrades a subsample, and agreement between the
two judges is reported in the paper.

## The grade ruling

The grade every result uses is a ruled grade, not the verdict the two-stage grader produced on its own. Reading
the graded records, the author found the stage-one rule and the judge in error on a share of responses whose
correctness is not in dispute, in both directions, mostly on numeric format and on lenient matches. A
deterministic ruling, applied before any estimate, corrects them with five rules. A paired-answer task is
regraded by a rule that checks both parts of the answer. A symbolic task is regraded by exact arithmetic at
fixed evaluation points. Any answer graded wrong whose canonical form equals the canonical form of the verified
answer is marked correct. On four tasks, accepts of the value the red herring plants are marked wrong.
A short list of other suspect accepts is marked wrong, and a short list of equivalent rejects is marked correct.
The ruling's output on the reference study is a per-response lookup that fixes the final-answer grade before any
estimate; it travels with the paper's replication materials, not with this benchmark. The ruling code encodes the
verified answers of the tasks it regrades and is available under the data-use agreement, see DATA_ACCESS.md.

## What the red herring measures

The loss comes from distraction. The reference study adds a second arm, a common red
herring, a single text of four true results from published economics inserted into every task at the same
point as the tailored one. Both red herrings leave the problem unchanged by the same verified standard, changing
no parameter and no answer. What differs is how much each pulls the reasoning toward a wrong line of argument
for the task at hand, and that pull is distraction. The common red herring, which cannot be plausible for every
task at once, has an effect indistinguishable from zero, so neither added length nor economic content in general
lowers accuracy. Each tailored red herring is also graded, before its effect is seen, on a
three-level scale: class A is an orthogonal fact the solution never uses, class B is a true statement next to
the task's mechanism that says nothing about the direction of the answer, and class C is a plausible but
incorrect argument that bears on the task's own answer. The damage is confined to class C.

## Estimand

The primary outcome is answer correctness, one when the final answer matches the verified answer under the
ruled grade. The benchmark identifies the causal effect of the red herring within task, from the difference
between the treatment and control versions of the same problem, absorbing everything common to a problem's
four versions with task fixed effects and everything common to a model with model fixed effects. Standard
errors are double-clustered by task and by model.

## Reasoning-behavior taxonomy

Each model is labeled by its default reasoning behavior, verified against provider documentation, gateway
routing metadata and an empirical probe. Type 1 emits a separate reasoning-token stream by default. Type 2
accepts a reasoning parameter but emits none under these default calls. Type 3 has no reasoning mode. Since
neither Type 2 nor Type 3 produces a reasoning trace by default, the analysis groups them together as
non-reasoning and sets them against the reasoning models of Type 1. The label is behavioral and is not a claim
about whether a model can reason.
