# promptbench

Code and supplementary material for the paper *"Robustness Evaluation of the FLAN-T5 Model Against Prompt Variations in Text Classification Tasks"* (SIET 2026, paper ID 1571312531).

This study evaluates the robustness of Flan-T5 Large against four categories of prompt variation (rewording, style change, noise injection, adversarial attack) on three text classification benchmarks (SST-2, MNLI, RTE), using the [PromptBench](https://github.com/microsoft/promptbench) framework.

## Repository structure

- [`notebooks/`](notebooks) — Kaggle notebooks (with saved outputs) used to run the SST-2, MNLI, and RTE experiments reported in the paper.
- [`appendix/`](appendix) — supplementary material referenced from the paper: full prompt templates and output-projection rules, and per-class precision/recall/F1 and confusion matrices for each dataset.

## Notes on reproducing results

- Model: `google/flan-t5-large`, accessed via Hugging Face, `temperature=0.3`, `max_new_tokens=50`.
- Each prompt is evaluated for 10 repeated runs; mean and standard deviation across runs are reported.
- SST-2 and RTE use their full validation splits (872 and 277 instances). MNLI uses a stratified random subsample of 3,600 instances (1,200 per class, fixed seed) drawn from the combined matched/mismatched validation split (19,647 instances total), for computational feasibility.
- Outputs that cannot be mapped to a valid label by the projection function are scored as incorrect (not excluded), and are never treated as an additional phantom class when computing macro F1.
