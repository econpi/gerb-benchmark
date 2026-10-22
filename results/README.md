# GERB results

**From sixty problems to fifty-nine in the results.** GERB is sixty problems, and the reference study fielded
all sixty: 38 models, four versions of every problem, five waves, 45,600 planned responses. The tables below are
the paper's tables, and the paper estimates on fifty-nine of the sixty. Of the sixty problems, fifty-nine carry a
passage that leaves every assumption and the final answer unchanged, and these fifty-nine are the estimation sample
(44,652 scored responses). The sixtieth carries a red herring that changes its answer, so it falls outside the
screen. Every number in these files is on the fifty-nine tasks under the ruled grade (see PROTOCOL.md). The files
contain model labels and statistics only, no problem text.

- `gerb_treatment_effects.csv` the four-column build-up of the main specification, the red-herring coefficient
  and the explanation-request coefficient with standard errors double-clustered by task and model.
- `gerb_robustness.csv` the red-herring coefficient under every specification, sample, grader and clustering
  scheme of the robustness battery, including the wild cluster bootstrap interval.
- `gerb_summary_by_condition.csv` accuracy and the graded indicators for each of the four experimental conditions.
- `gerb_by_model.csv` each model's reasoning type, scored responses, accuracy, control accuracy, red-herring
  accuracy and the raw per-model red-herring gap.
