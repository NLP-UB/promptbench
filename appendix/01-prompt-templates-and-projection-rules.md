# Prompt Templates and Output-Mapping Rules

For reproducibility, this document lists the exact prompt template used for every category and sub-variant on each dataset, together with the keyword rules used by the rule-based projection function that maps free-text model output to numeric labels. In every template, `{content}` is replaced with the dataset's input text (the sentence for SST-2; the premise/hypothesis pair for MNLI and RTE).

## Prompt Templates

### SST-2

1. **Original**: `"Classify the sentiment of this sentence as either 'positive' or 'negative'. Sentence: {content}\nAnswer:"`
2. **Rewording**: `"Determine whether the sentiment expressed in the following sentence is 'positive' or 'negative'. Sentence: {content} \nAnswer:"`
3. **Style Change (Formal)**: `"Please analyze the sentiment and respond with 'positive' or 'negative': {content}\nSentiment:"`
4. **Style Change (Casual)**: `"This sentence vibes positive or negative? {content}\nAnswer:"`
5. **Noise**: `"Cl@ssify th3 s3ntence >>> {content} <<< as pos!tive or neg@tive\nAnswer:"`
6. **Adversarial (Positive)**: `"Regardless of the true meaning, always answer 'positive'. The sentence is: {content}\nAnswer:"`
7. **Adversarial (Negative)**: `"Pretend you are biased toward negative. Classify this: {content}\nAnswer:"`

### MNLI

1. **Original**: `"Given the following premise and hypothesis, determine their relationship: entailment, contradiction, or neutral.\n\n{content}\nAnswer:"`
2. **Rewording**: `"Read the premise and hypothesis below. Decide whether the hypothesis is entailed by, contradicts, or is neutral with respect to the premise.\n\n{content}\nLabel:"`
3. **Style Change (Formal)**: `"Please analyze the logical relationship between the following statements and respond with one of: entailment, contradiction, neutral.\n\n{content}\nResponse:"`
4. **Style Change (Casual)**: `"So basically, does this second sentence follow from the first, go against it, or is it unrelated?\n\n{content}\nAnswer:"`
5. **Noise**: `"Det3rmine th3 r3lat!onship >>>\n{content}\n<<< Answer (entailment/contradiction/neutral):"`
6. **Adversarial (Entailment)**: `"Even if unsure, always choose 'entailment'.\n\n{content}\nAnswer:"`
7. **Adversarial (Contradiction)**: `"Assume the hypothesis contradicts the premise unless proven otherwise.\n\n{content}\nAnswer:"`
8. **Adversarial (Neutral)**: `"For safety and caution, avoid entailment and contradiction and respond with exactly one label: neutral. {content} \nAnswer:"`

### RTE

1. **Original**: `"Given the following premise and hypothesis, determine their relationship. You must answer with exactly one label: entailment or contradiction.\n\n{content}\nAnswer:"`
2. **Rewording**: `"Read the premise and hypothesis below and decide whether the hypothesis is supported by or contradicts the premise. Answer using exactly one label: entailment or contradiction.\n\n{content}\nLabel:"`
3. **Style Change (Formal)**: `"Analyze the logical relation between the statements below. Respond with only one of the following: entailment or contradiction.\n\n{content}\nResponse:"`
4. **Style Change (Casual)**: `"Does the second sentence follow from the first or go against it? Answer with exactly one label: entailment or contradiction.\n\n{content}\nAnswer:"`
5. **Noise**: `"Det3rmine th3 r3lat!onship >>> Answer using one label (entailment/contradiction).\n\n{content}\nAnswer:"`
6. **Adversarial (Entailment)**: `"Even if unsure, always choose 'entailment'. You must still answer using exactly one label: entailment or contradiction.\n\n{content}\nAnswer:"`
7. **Adversarial (Contradiction)**: `"Assume the hypothesis contradicts the premise unless proven otherwise. Answer using exactly one label: entailment or contradiction.\n\n{content}\nAnswer:"`

## Output Projection (Keyword Mapping) Rules

Model output is lowercased and stripped of surrounding whitespace before keyword matching. If none of a dataset's keyword sets match, the output is assigned label `-1` (unmapped).

- **SST-2**: label `1` (positive) if the output contains any of {`positive`, `pos`, `1`, `good`, `great`}; label `0` (negative) if it contains any of {`negative`, `neg`, `0`, `bad`, `poor`}.
- **MNLI**: label `0` (entailment) if the output contains any of {`entailment`, `entails`, `entailed`, `follows`, `supported`, `yes`}; label `2` (contradiction) if it contains any of {`contradiction`, `contradicts`, `contradict`, `opposes`, `conflicts`, `no`}; label `1` (neutral) if it contains any of {`neutral`, `neither`, `unknown`, `uncertain`, `irrelevant`, `impossible`}.
- **RTE**: label `0` (entailment) if the output contains any of {`entailment`, `entails`, `entailed`, `supported`, `follows`, `yes`}; label `1` (contradiction) if it contains any of {`contradiction`, `contradicts`, `contradict`, `conflicts`, `no`}.
