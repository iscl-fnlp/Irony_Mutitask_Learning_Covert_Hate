# Irony_Mutitask_Learning_covert_Hate
Irony-Aware Multitask Learning for Implicit Hate Speech


**implicit/covert hate speech**: the hateful meaning is conveyed indirectly rather than necessarily stated overtly.

RQ1. Is Irony as  implicit hate-speech category is the hardest for a fine-tuned RoBERTa model to detect?
How does the model’s misclassification behaviour look across implicit hate-speech categories? Specifically, which categories are most frequently confused with one another?
RQ2.Does knowledge of irony help improve implicit hate-speech classification through multitask learning?

## Hate Speech Categories
* **Grievance** — Complaining or blaming a group for a problem: “They are taking our jobs”
* **Incitement** — Encouraging people to act against a group. “Send them all back.”
* **Inferiority** — Saying or implying that a group is less capable or less worthy. “They are less intelligent.”
* **Irony** — Using irony, sarcasm, humor, or satire to demean a group. “I’m not racist, I just hate them.”
* **Stereotypes** — Linking a group to a negative general belief or characteristic. “They are all lazy.”
* **Threats** — Suggesting or expressing harm toward a group. “They should be afraid of us.”



## Dataset for experiment 1
The project uses the **Implicit Hate Speech (IHC)** dataset introduced by ElSherief et al.
Dataset: [SALT-NLP/implicit-hate](https://github.com/SALT-NLP/implicit-hate)
The original implicit-hate portion contains **6,346 tweets**:

| Category    | Tweets |     % |
| ----------- | -----: | ----: |
| Grievance   |  1,538 | 24.2% |
| Incitement  |  1,269 | 20.0% |
| Stereotypes |  1,133 | 17.9% |
| Inferiority |    863 | 13.6% |
| Irony       |    797 | 12.6% |
| Threats     |    666 | 10.5% |
| Other       |     80 |  1.2% |

`extra_implicit_class` is an additional label provided by the IHC dataset.

## Data Preparation
The data was divided into **training, development, and test sets**, preserving the original class distribution.The final test set contains **627 examples**:

| Category    | Test examples |
| ----------- | ------------: |
| Grievance   |           154 |
| Incitement  |           127 |
| Stereotypes |           114 |
| Inferiority |            87 |
| Irony       |            79 |
| Threats     |            66 |

## Model
A pretrained **RoBERTa** model was fine-tuned for six-class classification.The test set was then used only for evaluation.

## Results 1.
The model correctly classified **406 / 627 (64.7%)** examples and misclassified **221 / 627 (35.3%)**.Accuracy: 64.75%
Macro-F1: 0.6479.
Among the six categories, **Incitement** was the most difficult to detect based on F1 score (**0.6047**), followed by **Inferiority (0.6199)** and **Irony (0.6443)**.

| Category    | Precision | Recall |     F1 |
| ----------- | --------: | -----: | -----: |
| Grievance   |    0.6824 | 0.6558 | 0.6689 |
| Incitement  |    0.5954 | 0.6142 | 0.6047 |
| Stereotypes |    0.6726 | 0.6667 | 0.6696 |
| Inferiority |    0.6310 | 0.6092 | 0.6199 |
| Irony       |    0.6857 | 0.6076 | 0.6443 |
| Threats     |    0.6173 | 0.7576 | 0.6803 |

## Major Confusions
The largest true → predicted errors were:

| True → Predicted         | Errors |
| ------------------------ | -----: |
| Grievance → Incitement   |     22 |
| Incitement → Grievance   |     17 |
| Incitement → Stereotypes |     15 |
| Stereotypes → Grievance  |     15 |
| Grievance → Stereotypes  |     14 |
| Inferiority → Irony      |     14 |
| Incitement → Threats     |     12 |
| Irony → Inferiority      |     12 |
| Stereotypes → Incitement |     11 |


