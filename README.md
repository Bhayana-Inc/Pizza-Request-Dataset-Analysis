This repo contains code and analysis for **predicting the success of altruistic requests** on Reddit’s r/Random_Acts_Of_Pizza (RAOP) and comparing model performance to the paper’s baselines. :contentReference[oaicite:0]{index=0}  

The assignment trains and evaluates **four separate models** and then reflects on what types of features (language vs. user behavior) actually help with prediction.


## Models Implemented

All models predict whether a request received pizza (`requester_received_pizza` as 0/1).

1. **Model 1 – n-grams (text only)**
   - Features: unigrams + bigrams from `request_text`.
   - Goal: capture lexical / phrasing patterns in the request.
   - Performance: moderate; better than random, but worse than user-behavior features.

2. **Model 2 – Activity & Reputation (best model)**
   - Features: user/account-level signals (account age, karma-like stats, post counts, RAOP participation, etc.).
   - Goal: capture **credibility and engagement** of the requester.
   - Performance: **best overall** (highest accuracy, F1, AUC ≈ 0.78), robust to class imbalance.

3. **Model 3 – Narratives**
   - Features: counts / normalized frequencies of words from narrative lexicons (desire, family, job, money, student).
   - Goal: represent *what kind of story* the requester tells.
   - Performance: poor; essentially predicts almost all as negative (no pizzas).

4. **Model 4 – Moral Foundations**
   - Features: moral-foundation lexicons (care, loyalty, authority, sanctity) applied to request text.
   - Goal: detect moral language and ethical framing.
   - Performance: worst model; AUC < 0.5, very low recall for successful requests.

The notebook also compares these numbers to the ROC AUC baselines from the RAOP paper and discusses why **social/activity features** outperform most **pure language** feature sets. :contentReference[oaicite:1]{index=1}  

---

## Repo Layout (expected)

```text
.
├── assignment3.ipynb          # Main notebook: training, eval, and comparison to paper
├── pizza_request_dataset.json # RAOP dataset subset
├── narratives/                # (If used) narrative wordlists (desire, family, job, money, student)
├── MoralFoundations.dic       # (If used) moral foundations dictionary
└── ASSIGNMENT III Rachit Bhayana.pdf  # Written analysis & comparison to paper
