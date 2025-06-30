# Credit Risk Probability Model
## Project Structure

```
.gitignore
README.md
requirments.txt
.github/
    workflows/
        py.yml
data/
    processed/
    raw/
        data.csv
notebook/
script/
src/
```

- **.github/**: GitHub Actions workflows for CI/CD.
- **data/**: Contains raw and processed datasets.
- **notebook/**: Jupyter notebooks for exploratory analysis and prototyping.
- **script/**: Standalone scripts for data processing or model training.
- **src/**: Source code for the main application and modules.

## Requirements

Install dependencies with:
```sh
pip install -r requirments.txt
```

#  Credit Scoring Business Understanding

---

##  Overview

This project explores **credit scoring model development** in a regulated financial context.  
It discusses the importance of model interpretability, the use of proxy variables for rare default events, and the trade-offs between simple and complex modeling approaches.

---

###  Basel II Accord & Model Interpretability

> **How does the Basel II Accord's emphasis on risk measurement influence our need for an interpretable and well-documented model?**

The Basel II Accord, particularly through its **Pillar 1** (Internal Ratings-Based approach) and **Pillar 2** (Supervisory Review), mandates that banks using their own models for capital calculations demonstrate their risk measurement systems are **robust, logical, and transparent**.  
This directly influences the need for an **interpretable model** where the impact of each variable on the final risk score is clear. An interpretable model enables the bank to:

- ✅ Justify decisions to auditors and regulators  
- ✅ Conduct effective model validation and stress testing  
- ✅ Ensure accountability by explaining outcomes to stakeholders  

> A "black-box" model, regardless of its accuracy, would not pass supervisory review because its inner workings are not auditable or provably sound and non-discriminatory.

---

### 🕵️‍♂️ Proxy Variables & Business Risks

> **Since we lack a direct "default" label, why is creating a proxy variable necessary, and what are the potential business risks of making predictions based on this proxy?**

A direct "default" label, such as an account charged off or entering bankruptcy, is often a rare event that occurs long after initial signs of distress.  
Creating a **proxy variable** (e.g., a loan being 90 days past due) is necessary because it:

- ⚡ Provides an earlier warning sign of credit deterioration  
- ⚡ Creates a larger and more balanced dataset for training a predictive model, as proxy events are more frequent than terminal defaults  

However, relying on a proxy carries significant business risks:

- **Risk of False Positives:**  
  The model might flag a customer based on the proxy event (e.g., 90 days late) who would have eventually self-cured and repaid the loan.  
  This can lead to unnecessary collection actions, damaged customer relationships, and unwarranted tightening of credit for potentially good customers.

- **Model-Concept Mismatch:**  
  The factors that predict the proxy may not be the same as those that predict true financial loss.  
  The model could become very good at predicting a temporary delinquency but fail to identify risks (like fraud) that lead to a sudden, total default.

---

### ⚖️ Trade-offs: Simple vs. Complex Models

> **What are the key trade-offs between using a simple, interpretable model (like Logistic Regression with WoE) versus a complex, high-performance model (like Gradient Boosting) in a regulated financial context?**

In a regulated financial context, choosing between simple and complex models involves balancing **performance and compliance**.

#### Simple Models (e.g., Logistic Regression with Weight of Evidence - WoE):

- **Pros:**
  - 🟢 Highly interpretable and transparent, with a clear and often monotonic contribution from each variable, making explanations to regulators easy.
  - 🟢 Stable, well-understood, and straightforward to document, which significantly increases the likelihood of passing supervisory review.

- **Cons:**
  - 🔴 Lower predictive power.
  - 🔴 May not capture complex, non-linear relationships in the data, potentially leading to less precise risk segmentation and higher capital requirements than necessary.

#### Complex Models (e.g., Gradient Boosting):

- **Pros:**
  - 🟢 Deliver superior predictive performance by capturing complex, non-linear relationships in the data.
  - 🟢 Enable more accurate risk assessment, improved portfolio management, and potentially lower capital allocation.

- **Cons:**
  - 🔴 Often operate as "black-box" models, making it challenging to explain individual decisions—a significant barrier for regulatory approval.
  - 🔴 More susceptible to overfitting and may exhibit less stability compared to simpler models.

---

> **The fundamental trade-off is between _Performance_ and _Interpretability_.**  
> In highly regulated banking environments, regulatory approval is paramount. As a result, a slightly less powerful but fully transparent model is often the only viable choice for official capital calculations.  
> 
> An interpretable model ensures that the contribution of each variable to the final risk score is clear. This transparency enables the bank to:
> - Justify decisions to auditors and regulators
> - Conduct effective model validation and stress testing
> - Ensure accountability by explaining outcomes to stakeholders

A "black-box" model, regardless of its accuracy, is unlikely to pass supervisory review due to its lack of transparency and auditability.