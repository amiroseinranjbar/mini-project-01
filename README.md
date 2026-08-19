# 💳 Credit Card Fraud Detection

## 📌 Project Overview

This project focuses on detecting fraudulent credit card transactions using machine learning.

The dataset is highly imbalanced, meaning that legitimate transactions are much more common than fraudulent ones. Therefore, the main goal is not simply to achieve high accuracy, but to correctly identify fraudulent transactions while keeping false alarms under control.

Several machine learning models are evaluated and compared, including:

- Logistic Regression
- Decision Tree
- K-Nearest Neighbors (KNN)
- Random Forest
- XGBoost
- Ensemble Model

The models are evaluated mainly using **Precision, Recall, F1-score, and PR-AUC**.

---

# 🧠 Hypothesis Before Modeling

### 1. Which model do you expect to perform best?

I expect the more advanced nonlinear models, such as **Random Forest and XGBoost**, to perform better than Logistic Regression because they can capture more complex relationships between the features.

I also expect KNN to perform reasonably well because fraud detection can depend on similarities between transactions.

---

### 2. Which metric is more important?

**Recall** is particularly important because a false negative means that a fraudulent transaction is classified as legitimate.

However, maximizing Recall alone can produce many false positives. Therefore, **F1-score** is also important because it provides a balance between Precision and Recall.

---

### 3. What happens if the model predicts all transactions as legitimate?

The model would achieve a very high **Accuracy** because legitimate transactions dominate the dataset.

However, its **Recall for the fraud class would be 0**, since it would fail to detect any fraudulent transaction.

Therefore, Accuracy is not a reliable metric for this highly imbalanced dataset.

---

### 4. Does feature scaling affect KNN?

Yes. I expect feature scaling to have a significant effect on KNN because KNN relies directly on distances between samples.

Without scaling, features with larger numerical ranges could dominate the distance calculation.

---

### 5. Do you expect the Decision Tree to overfit?

Yes. Decision Trees can easily become complex and fit noise in the training data, especially when the tree is allowed to grow deeply.

Therefore, parameters such as `max_depth`, `min_samples_split`, and `min_samples_leaf` need to be tuned to control overfitting.

---

# 📊 After Training Analysis

### Was the initial hypothesis correct?

The results showed that the nonlinear models performed better than Logistic Regression for detecting the minority fraud class.

The best-performing models achieved higher **Recall and F1-score** than Logistic Regression, supporting the initial hypothesis that more flexible models can capture relationships that a linear model may miss.

---

### Which model performed best?

Among the simple models, **KNN** achieved a fraud-class:

- **Precision:** 0.96
- **Recall:** 0.72
- **F1-score:** 0.82

Decision Tree achieved an F1-score of **0.80**, while Logistic Regression achieved **0.69**.

Therefore, KNN performed better than the other simple baseline models in this experiment.

---

### Which metric was most informative?

**Recall and F1-score** were more informative than Accuracy.

Recall shows how many fraudulent transactions were successfully detected, while F1-score provides a balance between detecting fraud and avoiding false alarms.

---

### How did class imbalance affect the results?

The dataset contains a very large number of legitimate transactions and only a small number of fraudulent transactions.

As a result, models can achieve almost perfect Accuracy while still missing a considerable number of fraudulent transactions.

This is why the performance of the minority class was analyzed separately.

---

### False Positives vs. False Negatives

A **False Positive** occurs when a legitimate transaction is incorrectly classified as fraud.

A **False Negative** occurs when a fraudulent transaction is classified as legitimate.

In fraud detection, False Negatives are particularly important because they represent undetected fraud. However, too many False Positives can also negatively affect the user experience.

Therefore, the goal is to achieve a suitable balance between Precision and Recall rather than optimizing only one of them.