# ✈️ Predicting Airline Passenger Satisfaction

A supervised machine learning project that predicts whether an airline passenger will be **satisfied or dissatisfied**, using real-world survey data from 136,000+ journeys.

> **Team:** Aqeela Herz · Safa Aljeshi · Zainab Almutawa — 2026

---

## 📌 Problem Statement

An airline is losing customers, with satisfaction scores falling below the industry average of 65–70% (ACSI benchmark). This project builds a classification model to predict passenger satisfaction across key service areas, with a target accuracy of **80%+**, to deliver actionable insights and reduce churn.

---

## 📊 Dataset Overview

| Attribute | Value |
|-----------|-------|
| Total records | 136,000 passenger journeys |
| Features | 25 attributes per passenger |
| Service rating columns | 14 touchpoints (rated 0–5) |
| Missing values | 415 entries in arrival delay only |

**Feature categories:**

- **Who is flying** — Age, gender, customer type (new vs. returning), travel type (business vs. personal), cabin class
- **Trip details** — Flight distance, departure delay, arrival delay
- **Service ratings (0–5)** — Wi-Fi, booking, check-in, boarding, seat comfort, food, entertainment, cleanliness, baggage

---

## 🧹 Data Cleaning

- Standardized categorical labels (fixed casing and whitespace inconsistencies)
- Stripped embedded unit strings (`"miles"`, `"minutes"`) to convert columns to true numerics
- Imputed 415 missing arrival-delay values using departure delay (correlation = 0.97)
- Dropped redundant columns (IDs, unnamed indices, near-duplicate arrival-delay column)

---

## 🔍 EDA Highlights

- **Delays are highly correlated** — departure and arrival delays share a ~0.97 correlation
- **Business class & returning customers** report significantly higher satisfaction than economy or personal-travel passengers
- **Dataset is balanced** — 56% neutral/dissatisfied vs. 44% satisfied; no resampling needed
- **Online Boarding** is the strongest positive driver (+0.55 correlation with satisfaction)
- **Gate Location** has zero measurable impact; **Schedule Convenience** slightly reduces satisfaction (−0.05)
- **Most significant feature:** Cabin class (Business vs. Economy)
- **Least significant feature:** Gender

---

## ⚙️ Preprocessing

| Step | Description |
|------|-------------|
| One-hot encoding | Converts categorical variables (e.g. cabin class, customer type) into binary flag columns |
| Standard scaling | Normalises all numeric features to the same range so large-valued features (e.g. flight distance) don't dominate ratings (0–5) |

---

## 🤖 Modelling

Two classification algorithms were benchmarked:

### Baseline Results

| Model | Accuracy | Precision | Recall | F1 Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression | 87.57% | 0.872 | 0.837 | 0.854 |
| K-Nearest Neighbors | 92.95% | 0.951 | 0.884 | 0.916 |

### After Hyperparameter Tuning (GridSearchCV)

| Model | Accuracy | Precision | Recall | F1 Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression | 87.55% | 0.872 | 0.836 | 0.854 |
| **K-Nearest Neighbors** | **94.35%** | **0.955** | **0.913** | **0.933** |

KNN was selected as the final model. Optimal configuration: **K=9**, Manhattan distance, distance-weighted voting. Cross-validation accuracy reached **94.1%** with a specificity of ~96.7%.

---

## 🏆 Final Result

> **94.3% accuracy** on the held-out test set

The tuned KNN model correctly classifies ~94 out of every 100 passengers. When it predicts "satisfied", it is right **95.5% of the time**, and it catches **91.3%** of all genuinely satisfied flyers.

---

## 💡 Business Recommendations

### Invest Here
| Priority | Feature | Insight |
|----------|---------|---------|
| 1 | **Online Boarding** | Strongest controllable satisfaction signal |
| 2 | **Returning Customer Loyalty** | Loyal customers signal trust — protect this base |
| 3 | **In-flight Wi-Fi** | Current average: 2.7/5 — the biggest upside opportunity |

### Watch These Risk Factors
| Risk | Detail |
|------|--------|
| Personal/leisure travel | Strong negative satisfaction signal; leisure flyers expect more |
| Economy class | Aligns with dissatisfaction more than any other cabin class |
| Low service ratings | Especially Wi-Fi and online booking |

---

## 👥 Authors

| Name | 
|------|
| Aqeela Herz |
| Safa Aljeshi |
| Zainab Almutawa |
