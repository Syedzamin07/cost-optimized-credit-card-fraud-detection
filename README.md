# 💳 Cost-Optimized Credit Card Fraud Detection

**A business-first fraud detection system focused on minimizing financial loss, not maximizing vanity metrics.**

---

## 📝 The Problem: A Game of Unequal Mistakes

In credit card fraud detection, not all errors carry the same cost.

- Missing a fraudulent transaction means **direct financial loss and reputational damage**.
- Blocking a legitimate customer creates **operational cost and churn risk**.

Most machine learning projects optimize for technical metrics like **Accuracy**, which are misleading in highly imbalanced problems.

**This project reframes fraud detection as a cost-minimization problem.**

---

## 💰 Decision Framework (Business Lens)

| Outcome | Business Impact | Assumed Cost* |
|------|---------------|---------------|
| False Negative (Missed Fraud) | Liability + chargeback | **$100** |
| False Positive (Blocked Customer) | Support cost + churn risk | **$5** |

**Objective:**  
Find the operating point that minimizes **total expected financial loss**, not error count.

---

## 🚀 Solution Strategy

### 1️⃣ Leakage-Safe Model Design
A common fraud modeling mistake is applying resampling techniques (SMOTE) **before** data splitting, which causes data leakage.

I used a strict **`imblearn` pipeline** to ensure:
- Scaling and SMOTE are applied **only on training data**
- The test set remains a realistic proxy for production data

---

### 2️⃣ Using the Right Metric: PR-AUC
Fraud represents only **0.17%** of transactions.

- Accuracy and ROC-AUC appear artificially high due to class imbalance
- I prioritized **Precision–Recall AUC (≈ 0.85)**, which directly measures fraud detection quality

This confirms the model can meaningfully separate fraud from legitimate transactions.

---

### 3️⃣ Threshold Optimization: The ROI Layer
Instead of defaulting to a 0.50 probability threshold, I performed a **threshold sweep**:

- Simulated **100 decision thresholds**
- Calculated total financial loss at each point
- Identified the **cost-optimal operating threshold**

This converts model scores into **actionable business decisions**.

---

## 📊 Results (Evaluated on Test Set, Under Stated Assumptions)

| Strategy | Decision Rule | Relative Financial Impact |
|--------|---------------|--------------------------|
| Naive Baseline | Allow all transactions | Reference (100%) |
| Standard ML | Default threshold (0.50) | ~10% of baseline loss |
| **Optimized ML** | **Cost-optimized threshold (0.69)** | **~80% reduction** |

**Key Insight:**  
Default thresholds are arbitrary. Explicitly pricing errors unlocks substantial financial improvement without retraining the model.

---

## 🕵️‍♂️ Explainability: Why Transactions Are Flagged

Fraud models cannot operate as black boxes.

I integrated **SHAP** to provide:
- **Global explanations:** Which behavioral signals the model relies on most
- **Local explanations:** Why a specific transaction was flagged

This enables fraud analysts to **validate, override, or defend decisions**, supporting regulatory and operational requirements.

---

## 📂 Repository Structure:

notebooks/
- data_understanding.ipynb  
  Sanity checks, fraud ratio validation, and feature context

- baseline_analysis.ipynb  
  Establishes the “do nothing” financial cost floor

- model_pipeline.ipynb  
  Leakage-safe ML pipeline with PR-AUC evaluation

- cost_optimization.ipynb  
  Threshold sweep to minimize total expected financial loss

- explainability.ipynb  
  SHAP-based global and local explanations for analyst review

decision_framework.md  
Plain-English documentation of business assumptions and cost logic

