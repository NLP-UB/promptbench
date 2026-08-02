# SST-2 Class-wise Results

This document reports per-class F1 for all seven SST-2 prompts, and the confusion matrix for the two prompts with the highest unmapped rates (Noise and Adversarial (Negative)), pooled across the ten runs of each prompt (8,720 predictions per prompt: 10 runs × 872 instances). See Table 1 in the paper for the corresponding accuracy/F1/unmapped-rate summary per prompt.

## Per-class F1-score for every SST-2 prompt (pooled across 10 runs)

| Prompt | Negative F1 | Positive F1 |
|---|---|---|
| Original | 0.938 | 0.943 |
| Rewording | 0.942 | 0.946 |
| Style Change (Formal) | 0.941 | 0.945 |
| Style Change (Casual) | 0.940 | 0.945 |
| Noise | 0.566 | 0.423 |
| Adversarial (Positive) | 0.859 | 0.892 |
| Adversarial (Negative) | 0.415 | 0.521 |

## Confusion matrix, Noise prompt

(rows: true label; columns: predicted; pooled across 10 runs, 8,720 predictions; "Unm." = unmapped output)

| True \\ Predicted | Negative | Positive | Unm. |
|---|---|---|---|
| Negative | 1764 | 54 | 2462 |
| Positive | 193 | 1205 | 3042 |

## Confusion matrix, Adversarial (Negative) prompt

(rows: true label; columns: predicted; pooled across 10 runs, 8,720 predictions; "Unm." = unmapped output)

| True \\ Predicted | Negative | Positive | Unm. |
|---|---|---|---|
| Negative | 1228 | 17 | 3035 |
| Positive | 414 | 1569 | 2457 |

## Interpretation

Both tables show the same qualitative pattern: roughly 55–69% of instances in each true class produced unmapped output, and among the *mapped* predictions, the model still showed a directional bias (toward negative under Noise, and away from negative under Adversarial (Negative) despite the prompt's explicit negative-bias instruction). This confirms that both prompts primarily disabled the model's ability to produce a parseable label, with any residual labeling bias a secondary effect.
