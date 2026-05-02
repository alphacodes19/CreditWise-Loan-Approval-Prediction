# 🏦 CreditWise Loan Approval Prediction System

> *"Can a machine decide faster, fairer, and smarter than a loan officer?"*
> This project builds an intelligent loan approval system for **SecureTrust Bank** using Machine Learning — predicting whether a loan application should be **Approved ✅** or **Rejected ❌** before final human review.

---

## 📌 Table of Contents

- [The Real-World Problem](#-the-real-world-problem)
- [Our Solution](#-our-solution)
- [Dataset Overview](#-dataset-overview)
- [Project Workflow](#-project-workflow)
- [Models Used](#-models-used)
- [Results & Evaluation](#-results--evaluation)
- [Tech Stack](#-tech-stack)
- [How to Run](#-how-to-run-this-project)
- [Project Structure](#-project-structure)
- [Key Learnings](#-key-learnings)
- [Future Improvements](#-future-improvements)

---

## 🔴 The Real-World Problem

**SecureTrust Bank** is a mid-sized financial company offering personal and home loans to customers across urban and rural regions of India. Every day, hundreds of customers apply for loans through online and branch applications.

Until now, the bank has relied on a **manual verification process** where loan officers evaluate each application by checking income proofs, employment details, credit history, and supporting documents.

### ❌ Why This is a Problem

This manual process is **slow, biased, and inconsistent** — leading to two costly mistakes:

| Problem | Consequence |
|---|---|
| 😟 Good customers sometimes get **rejected** | Loss of business and revenue |
| 😬 High-risk customers sometimes get **approved** | Financial losses and bad debt |

---

## ✅ Our Solution

The goal: build an **intelligent loan approval system** that:
1. Learns hidden patterns from thousands of past loan applications
2. Automatically analyses a new applicant's profile
3. Predicts — **Approve or Reject** — before it reaches a human officer

This makes loan decisions **faster ⚡, fairer ⚖️, and more consistent 🎯.**

---

## 📊 Dataset Overview

The dataset `loan_approval_data.csv` contains historical loan application records from SecureTrust Bank. Each row = one loan applicant.

### 📋 Features (Inputs to the model)

| Column | Type | Description |
|---|---|---|
| `Applicant_ID` | ID | Unique applicant identifier |
| `Applicant_Income` | Numerical | Monthly income of the applicant |
| `Coapplicant_Income` | Numerical | Monthly income of any co-applicant |
| `Employment_Status` | Categorical | Salaried / Self-Employed / Business |
| `Age` | Numerical | Age of the applicant |
| `Marital_Status` | Categorical | Married / Single |
| `Dependents` | Numerical | Number of financial dependents |
| `Credit_Score` | Numerical | Credit bureau score (higher = better) |
| `Existing_Loans` | Numerical | Number of already running loans |
| `DTI_Ratio` | Numerical | Debt-to-Income ratio (lower = less burden) |
| `Savings` | Numerical | Savings balance |
| `Collateral_Value` | Numerical | Value of asset offered as security |
| `Loan_Amount` | Numerical | Loan amount requested |
| `Loan_Term` | Numerical | Loan duration in months |
| `Loan_Purpose` | Categorical | Home / Education / Personal / Business |
| `Property_Area` | Categorical | Urban / Semi-Urban / Rural |
| `Education_Level` | Categorical | Graduate / Postgraduate / Undergraduate |
| `Gender` | Categorical | Male / Female |
| `Employer_Category` | Categorical | Govt / Private / Self |

### 🎯 Target (What we predict)

| Column | Value | Meaning |
|---|---|---|
| `Loan_Approved` | `1` | ✅ Loan Approved |
| `Loan_Approved` | `0` | ❌ Loan Rejected |

---

## 🔄 Project Workflow

```
📂 Raw Data (loan_approval_data.csv)
         │
         ▼
📥 Step 1 — Data Loading & Exploration
         Understand shape, types, and missing values
         │
         ▼
🧹 Step 2 — Data Cleaning
         Fill missing numbers  →  Mean value
         Fill missing categories  →  Most frequent value
         │
         ▼
📊 Step 3 — Exploratory Data Analysis (EDA)
         Pie chart   →  Class balance (Approved vs Rejected)
         Bar plots   →  Category-wise breakdowns
         Box plots   →  Detect outliers
         Histograms  →  Understand distributions
         Heatmap     →  Feature correlations
         │
         ▼
🔢 Step 4 — Encoding Categorical Variables
         Label Encoding   →  Education Level (has natural order)
         One-Hot Encoding →  Gender, Employment, Area, etc.
         │
         ▼
⚖️ Step 5 — Feature Scaling
         StandardScaler → Normalize all numerical values to same range
         │
         ▼
✂️ Step 6 — Train-Test Split
         80% Training  |  20% Testing
         │
         ▼
🤖 Step 7 — Model Training & Evaluation
         → Logistic Regression
         → K-Nearest Neighbors (KNN)
         → Naive Bayes
         │
         ▼
🔧 Step 8 — Feature Engineering
         Add  DTI_Ratio²  and  Credit_Score²  as new features
         Re-train all models and compare improvement
         │
         ▼
🏆 Best Model Selected!
```

---

## 🤖 Models Used

### 1. 📉 Logistic Regression
> A classic statistical model that estimates the *probability* of approval. It draws a decision boundary to separate "Approved" from "Rejected" applications.

- ✅ Highly interpretable — you can see which features matter most
- ✅ Fast to train and easy to explain
- ⚠️ Assumes a linear relationship between features and outcome

---

### 2. 👥 K-Nearest Neighbors (KNN)
> Classifies a new applicant by finding the **5 most similar applicants** in the training data and going with the majority vote.

- ✅ No assumptions about data distribution
- ✅ Naturally handles non-linear patterns
- ⚠️ Can be slower on very large datasets
- **Setting used:** `n_neighbors = 5`

---

### 3. 📐 Naive Bayes (Gaussian)
> A probability-based model rooted in **Bayes' Theorem**. It calculates the likelihood of approval given each feature independently.

- ✅ Very fast to train
- ✅ Works well even with limited data
- ⚠️ Assumes all features are independent of each other

---

## 📈 Results & Evaluation

Each model is measured on four metrics:

| Metric | Plain English | Why It Matters for Loans |
|---|---|---|
| **Accuracy** | % of total correct predictions | General performance measure |
| **Precision** | Of predicted *approvals*, how many were truly approved? | Avoid approving risky loans (financial loss) |
| **Recall** | Of all actual *approvals*, how many did we catch? | Avoid rejecting good customers (lost revenue) |
| **F1 Score** | Balance between Precision and Recall | Best single number for overall quality |

> 🏆 **Best Performing Model: Naive Bayes**
> Selected on **highest Precision** — in banking, approving a high-risk loan is far more damaging than missing a good applicant.

Models were evaluated **twice** — before and after Feature Engineering — to measure the impact of the new squared features.

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **Python 3.x** | Core programming language |
| **Pandas** | Data loading and manipulation |
| **NumPy** | Numerical computations |
| **Matplotlib** | Charts and visualizations |
| **Seaborn** | Statistical data visualization |
| **Scikit-learn** | ML models, preprocessing, and evaluation |
| **Jupyter Notebook** | Interactive development environment |

---

## 🚀 How to Run This Project

### Prerequisites
Python 3.7+ installed — [Download here](https://www.python.org/downloads/)

### Step 1 — Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

### Step 2 — Install required libraries
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Step 3 — Add the dataset
Place `loan_approval_data.csv` in the **same folder** as the notebook.

### Step 4 — Launch Jupyter Notebook
```bash
jupyter notebook
```

### Step 5 — Run the notebook
Open `Untitled.ipynb` → Click **Kernel → Restart & Run All** → Watch the magic! 🎉

---

## 📁 Project Structure

```
📦 creditwise-loan-approval/
 ┣ 📓 Untitled.ipynb              ← Main notebook (all code here)
 ┣ 📊 loan_approval_data.csv      ← Dataset (add manually)
 ┣ 📄 Problem_Statement.pdf       ← Original problem statement
 ┗ 📄 README.md                   ← You are here!
```

---

## 💡 Key Learnings

- **Data cleaning is foundational** — Missing values silently break models if not handled first.
- **EDA reveals the story** — Visualizing data showed `Credit_Score` and `DTI_Ratio` as the strongest predictors.
- **Encoding type matters** — Using Label Encoding on nominal data (like Gender) misleads models by implying a false numeric order.
- **Feature engineering adds value** — Squared terms captured non-linear relationships that linear models miss.
- **Choose metrics wisely** — In banking, **Precision** matters more than raw accuracy. A bad loan approved = real financial damage.
- **No single model wins always** — Comparing multiple models before choosing one is essential in practice.

---

## 🔮 Future Improvements

- [ ] Try advanced models: **Random Forest**, **XGBoost**, **LightGBM**
- [ ] Handle **class imbalance** using SMOTE if the dataset is skewed
- [ ] Perform **hyperparameter tuning** with GridSearchCV
- [ ] Add **k-fold cross-validation** for more robust evaluation
- [ ] Integrate **SHAP values** for model explainability — critical for regulatory audits
- [ ] Build a **Streamlit web app** so officers can enter applicant details and get instant predictions
- [ ] Deploy on cloud (**Render / Hugging Face Spaces**) for live access

---

## 👤 Author

Built as a **Minor Project** — CreditWise Loan System for SecureTrust Bank.

Drop a ⭐ if you found this useful!

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center"><i>Made with ❤️ | SecureTrust Bank × Machine Learning</i></p>
