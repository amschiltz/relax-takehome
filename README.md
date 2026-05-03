# Relax Data Science Take-Home Challenge

## Overview

This analysis identifies factors associated with user adoption using engagement and user attribute data.

An **adopted user** is defined as a user who logged into the product on **3 separate days within any 7-day period**.

Two datasets were provided:

- `takehome_users.csv` — user attributes  
- `takehome_user_engagement.csv` — login activity  

---

## Approach

### 1. Define Adoption

For each user, I checked for ≥3 unique login days within any rolling 7-day window and created a binary target variable:

- `adopted_user = 1` → adopted  
- `adopted_user = 0` → not adopted  

Adopted users comprised **13.8%** of the cohort, indicating class imbalance.

---

### 2. Feature Engineering

The following features were included:

- `creation_source` — how the user signed up  
- `was_invited` — derived from `invited_by_user_id`  
- `opted_in_to_mailing_list`  
- `enabled_for_marketing_drip`  
- `org_size` — number of users in the organization  

---

### 3. Modeling

A **Logistic Regression** model was used as a baseline due to its interpretability.

The modeling pipeline included:

- One-hot encoding for categorical features  
- Standardization for numeric features  
- Binary features passed through without transformation  
- Class weighting to address imbalance  

---

## Results

### Model Performance

- **ROC-AUC ≈ 0.60** → limited ability to distinguish between adopted and non-adopted users  

The model achieved:

- **Recall (adopted users): 0.76** → most adopters identified  
- **Precision (adopted users): 0.17** → many false positives  

This reflects a tradeoff driven by class imbalance and class weighting.

> Overall, the results suggest that the available features provide **limited predictive signal**, and that **early user behavior** may be more informative than static user attributes at signup.

---

## Key Predictors of Adoption

| Feature            | Effect on Adoption     | Approx. Change in Odds |
|--------------------|----------------------|------------------------|
| Google signup      | ↑ Higher likelihood  | +32%                  |
| Invited users      | ↑ Higher likelihood  | +30%                  |
| Personal projects  | ↓ Lower likelihood   | -45%                  |
| Larger org size    | ↓ Lower likelihood   | -27%                  |

---

## Interpretation

- **Signup pathway matters:** Users invited or signing up via Google are more likely to adopt  
- **Personal use case is weaker:** Personal project users are significantly less engaged  
- **Organizational context matters:** Larger organizations show lower individual adoption  
- **Marketing features have minimal impact**  

---

## Limitations

- Limited feature set: only user attributes available at signup were used  
- Early engagement signals (e.g., first-week activity) were not included  
- No hyperparameter tuning (focus was on an interpretable baseline model)  
- Time-based features derived from post-signup activity were excluded to avoid data leakage  

---

## Next Steps

With more time, I would:

- Incorporate early engagement signals (e.g., first-week activity), likely stronger predictors  
- Evaluate more flexible models (e.g., Random Forest, Gradient Boosting)  
- Explore interaction effects between signup method and organizational context  
- Conduct cohort analysis by signup source or organization  

---

## Repository Structure

```bash
relax-takehome/
├── relax_analysis.ipynb
├── README.md
└── requirements.txt
