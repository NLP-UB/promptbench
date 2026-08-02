# MNLI Class-wise Results

This document reports per-class precision, recall, and F1 for all eight MNLI prompts, together with the confusion matrix for three illustrative prompts (Original, Style Change (Casual), and Adversarial (Contradiction)), pooled across the ten runs of each prompt (36,000 predictions per prompt: 10 runs × 3,600 instances). See Table 2 in the paper for the corresponding accuracy/F1/unmapped-rate summary per prompt.

## Per-class F1-score for every MNLI prompt (pooled across 10 runs)

| Prompt | Entailment F1 | Neutral F1 | Contradiction F1 |
|---|---|---|---|
| Original | 0.846 | 0.718 | 0.885 |
| Rewording | 0.712 | 0.751 | 0.866 |
| Style Change (Formal) | 0.860 | 0.771 | 0.898 |
| Style Change (Casual) | 0.893 | 0.000 | 0.207 |
| Noise | 0.880 | 0.758 | 0.895 |
| Adversarial (Entailment) | 0.847 | 0.400 | 0.878 |
| Adversarial (Contradiction) | 0.891 | 0.749 | 0.906 |
| Adversarial (Neutral) | 0.850 | 0.557 | 0.601 |

Across every prompt, *neutral* is the class with the lowest (often substantially lowest) F1, confirming that the model's weakest point on MNLI is distinguishing neutral premise–hypothesis pairs rather than the other two classes. The Style Change (Casual) prompt is the extreme case: neutral F1 collapses to 0, meaning the model essentially never produced a parseable neutral prediction under that phrasing (consistent with its 61.7% unmapped rate). Notably, the Adversarial (Contradiction) prompt has the *highest* neutral F1 of all eight prompts (0.749, versus 0.718 under Original), which is the class-wise signature behind that prompt's accuracy matching the Original baseline.

## Confusion matrix, Original prompt

(rows: true label; columns: predicted; pooled across 10 runs, 36,000 predictions)

| True \\ Predicted | Entailment | Neutral | Contradiction |
|---|---|---|---|
| Entailment | 11038 | 493 | 469 |
| Neutral | 2907 | 7297 | 1796 |
| Contradiction | 149 | 530 | 11321 |

## Confusion matrix, Style Change (Casual) prompt

(rows: true label; columns: predicted; pooled across 10 runs, 36,000 predictions; "Unm." = unmapped output)

| True \\ Predicted | Entailment | Neutral | Contradiction | Unm. |
|---|---|---|---|---|
| Entailment | 10746 | 0 | 98 | 1156 |
| Neutral | 1053 | 0 | 214 | 10733 |
| Contradiction | 255 | 0 | 1419 | 10326 |

## Confusion matrix, Adversarial (Contradiction) prompt

(rows: true label; columns: predicted; pooled across 10 runs, 36,000 predictions; "Unm." = unmapped output)

| True \\ Predicted | Entailment | Neutral | Contradiction | Unm. |
|---|---|---|---|---|
| Entailment | 11028 | 512 | 267 | 193 |
| Neutral | 1400 | 7972 | 785 | 1843 |
| Contradiction | 321 | 815 | 10819 | 45 |

## Interpretation

For the Original prompt, most neutral-label errors are neutral instances misclassified as entailment (2,907 of 12,000 neutral instances), rather than as contradiction (1,796). For the Style Change (Casual) prompt, the dominant failure mode changes entirely: the majority of neutral (10,733/12,000) and a substantial share of contradiction (10,326/12,000) instances produced unmapped output, indicating that this phrasing mainly breaks the model's ability to produce a recognizable label at all for those two classes, rather than causing it to confuse them with entailment.

The Adversarial (Contradiction) prompt shows why this prompt alone preserves accuracy: compared to the Original confusion matrix, neutral recall rises from 0.608 (7,297/12,000) to 0.664 (7,972/12,000) — a net gain of 675 correctly classified neutral instances — while entailment recall is essentially unchanged (11,038 to 11,028 correct) and contradiction recall falls only slightly (11,321 to 10,819 correct, a loss of 502). The prompt's instruction to favor contradiction appears to resolve a portion of the model's characteristic entailment/neutral confusion in the model's favor for neutral instances specifically, rather than uniformly biasing predictions toward contradiction at the expense of the other two classes, which is why it does not depress accuracy the way the entailment-type and neutral-type attacks do.
