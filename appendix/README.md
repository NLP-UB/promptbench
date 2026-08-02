# Appendix: Robustness Evaluation of the Flan-T5 Model Against Prompt Variations in Text Classification Tasks

This folder contains supplementary material for the paper *"Robustness Evaluation of the FLAN-T5 Model Against Prompt Variations in Text Classification Tasks"* (SIET 2026, paper ID 1571312531), moved here from the paper's appendix to keep the main manuscript within the page limit. The paper itself links to this folder.

- [`01-prompt-templates-and-projection-rules.md`](01-prompt-templates-and-projection-rules.md) — the exact prompt template used for every category/sub-variant on each dataset, and the keyword rules used by the rule-based output-projection function.
- [`02-mnli-classwise-results.md`](02-mnli-classwise-results.md) — per-class precision/recall/F1 and confusion matrices for MNLI.
- [`03-sst2-classwise-results.md`](03-sst2-classwise-results.md) — per-class F1 and confusion matrices for SST-2.
- [`04-rte-classwise-results.md`](04-rte-classwise-results.md) — per-class F1 and confusion matrices for RTE.

The notebooks used to produce these results (SST-2, MNLI, RTE) are in the repository root / `notebooks` folder.
