# RTE Class-wise Results

This document reports per-class precision, recall, and F1 for all seven RTE prompts, and the confusion matrix for the two prompts with the highest unmapped rates (Style Change (Casual) and Noise), pooled across the ten runs of each prompt (2,770 predictions per prompt: 10 runs × 277 instances). See Table 3 in the paper for the corresponding accuracy/F1/unmapped-rate summary per prompt.

## Per-class F1-score for every RTE prompt (pooled across 10 runs)

| Prompt | Entailment F1 | Contradiction F1 |
|---|---|---|
| Original | 0.821 | 0.686 |
| Rewording | 0.829 | 0.705 |
| Style Change (Formal) | 0.832 | 0.718 |
| Style Change (Casual) | 0.883 | 0.605 |
| Noise | 0.876 | 0.500 |
| Adversarial (Entailment) | 0.828 | 0.707 |
| Adversarial (Contradiction) | 0.836 | 0.720 |

As on MNLI, one class is consistently weaker across nearly every RTE prompt: *contradiction* F1 trails *entailment* F1 by 0.11–0.14 under Original, Rewording, and both Style/Adversarial variants, and this gap widens sharply under Noise (0.876 vs. 0.500) and Style Change (Casual) (0.883 vs. 0.605).

## Confusion matrix, Style Change (Casual) prompt

(rows: true label; columns: predicted; pooled across 10 runs, 2,770 predictions; "Unm." = unmapped output)

| True \\ Predicted | Entailment | Contradiction | Unm. |
|---|---|---|---|
| Entailment | 1352 | 19 | 89 |
| Contradiction | 252 | 577 | 481 |

## Confusion matrix, Noise prompt

(rows: true label; columns: predicted; pooled across 10 runs, 2,770 predictions; "Unm." = unmapped output)

| True \\ Predicted | Entailment | Contradiction | Unm. |
|---|---|---|---|
| Entailment | 1295 | 19 | 146 |
| Contradiction | 201 | 443 | 666 |

## Interpretation

In both prompts, entailment instances are rarely unmapped (6.1% under Style Change (Casual), 10.0% under Noise) while contradiction instances are unmapped over a third to half of the time (36.7% and 50.8%, respectively). Combined with the confusion counts (252 and 201 contradiction instances misclassified as entailment), this indicates the model's baseline tendency to prefer entailment over contradiction on RTE (visible even under the Original prompt, where entailment recall is 0.992 versus contradiction recall of 0.526) is amplified, rather than reversed, by both perturbation types.
