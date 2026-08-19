# 🧠 Fraud Detection — Hypothesis Before Modeling

> 🎯 **Goal:** Predict fraudulent financial transactions using machine learning models.

---

## 🔬 7. Hypothesis Before Modeling

Before training the models, the following hypotheses were formulated based on the characteristics of the fraud detection problem.

---

### 1️⃣ Which model is expected to perform best?

🟦 **Hypothesis**

I expect the **XGBoost** model to perform best for fraud detection because it can capture complex and nonlinear relationships between features. 

I also expect **Random Forest** to perform strongly because combining multiple decision trees can reduce variance and improve generalization.

As baseline models, I expect **Decision Tree** and **KNN** to perform reasonably well, while **Logistic Regression** may have lower performance because of its linear decision boundary.

---

### 2️⃣ Which metric is more important?

🟩 **Hypothesis**

I expect **Recall** to be particularly important because failing to detect a fraudulent transaction means that a fraudulent transaction is classified as legitimate.

However, maximizing Recall alone is not sufficient. A model could achieve high Recall by predicting many legitimate transactions as fraudulent.

Therefore, **Precision and F1-score** should also be considered.

> **Main priority:** Recall  
> **Additional considerations:** Precision + F1-score

---

### 3️⃣ What happens if all transactions are predicted as legitimate?

🟥 **Hypothesis**

If the model predicts every transaction as **legitimate (class 0)**, the accuracy may still be extremely high because fraudulent transactions represent only a very small portion of the dataset.

However:

- **Recall → 0**
- **Precision → 0** for the fraud class
- **F1-score → 0** for the fraud class

Therefore, **Accuracy alone is misleading for this highly imbalanced dataset.**

---

### 4️⃣ Will feature scaling affect KNN?

🟨 **Hypothesis**

Yes. I expect feature scaling to significantly affect **KNN** performance.

KNN relies on distance calculations between samples. If different features have very different scales, features with larger numerical values can dominate the distance calculation.

Therefore, **StandardScaler** is expected to improve the performance and reliability of KNN.

---

### 5️⃣ Will the Decision Tree overfit?

🟧 **Hypothesis**

I expect the Decision Tree to have a risk of **overfitting**, especially when the tree becomes too deep.

A very deep tree can learn highly specific patterns from the training data instead of learning general patterns.

Therefore, hyperparameters such as:

- `max_depth`
- `min_samples_split`
- `min_samples_leaf`

should be tuned to control the complexity of the tree.

---

# 📊 After Training Analysis

After training and evaluating the models, the initial hypotheses can be compared with the actual results.

---

## 🏆 Model Performance

| Model | Precision | Recall | F1-score | Expected |
|:------|:---------:|:------:|:--------:|:--------:|
| 🌳 Decision Tree | 0.92 | 0.71 | 0.80 | Good |
| 📍 KNN | 0.96 | 0.72 | 0.82 | Good |
| 📈 Logistic Regression | 0.85 | 0.58 | 0.69 | Baseline |
| 🚀 XGBoost | — | — | — | Expected Best |
| 🌲 Random Forest | — | — | — | Expected Strong |

> **Note:** XGBoost and Random Forest results will be added after completing their experiments.

---

## 🔍 Was the Initial Hypothesis Correct?

The initial hypothesis that nonlinear models would perform better than Logistic Regression was supported by the results.

### 📌 Observed Results

**KNN** achieved:

- 🎯 Precision: **0.96**
- 🔎 Recall: **0.72**
- ⚖️ F1-score: **0.82**

**Decision Tree** achieved:

- 🎯 Precision: **0.92**
- 🔎 Recall: **0.71**
- ⚖️ F1-score: **0.80**

**Logistic Regression** achieved:

- 🎯 Precision: **0.85**
- 🔎 Recall: **0.58**
- ⚖️ F1-score: **0.69**

Therefore, among the evaluated baseline models, **KNN achieved the highest F1-score and Precision for the fraud class.**

---

## ⚖️ Class Imbalance

The dataset is **highly imbalanced**, with legitimate transactions greatly outnumbering fraudulent transactions.

This imbalance means that a model can achieve very high Accuracy while still failing to detect a significant number of fraudulent transactions.

Therefore, metrics such as:

> **Recall · Precision · F1-score · PR-AUC**

are more informative than Accuracy alone.

---

## 🚨 False Positives vs False Negatives

There are two important types of errors:

| Error | Meaning | Consequence |
|:------|:--------|:------------|
| ❌ **False Positive (FP)** | Legitimate transaction predicted as fraud | Unnecessary investigation / false alarm |
| ⚠️ **False Negative (FN)** | Fraudulent transaction predicted as legitimate | Fraud remains undetected |

For fraud detection, **False Negatives are particularly important** because they represent fraudulent transactions that were missed by the model.

However, reducing False Negatives by aggressively increasing Recall can increase False Positives.

Therefore, the main objective is to find a suitable balance between:

```text
Recall  ↔  Precision
       ↓
    F1-score