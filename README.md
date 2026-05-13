# 🛒 Customer Churn: End-to-End Production ML Pipeline

## **📋 Project Overview**
This repository implements an industry-standard predictive pipeline to identify customers at risk of leaving a service. Instead of just training a model, this project focuses on **ML Engineering**—building a systematic flow that automates data transformation and ensures the model is ready for real-world deployment[cite: 1]. 

The goal is to move from **"Raw Data"** to **"Actionable Predictions,"** allowing a business to target high-risk customers before they churn[cite: 1].

---

## **🏗️ Systematic Workflow**

### **1. Data Processing & Leakage Prevention**
*   **Feature Engineering:** Converted categorical target labels into binary format (1 for Churn, 0 for Stay).
*   **Data Leakage Prevention:** Crucially, the dataset was split into training and testing sets **before** any preprocessing. This ensures the model is evaluated on truly "unseen" data, a mechanical necessity for production-grade AI.
*   **Missing Value Strategy:** Implemented a **SimpleImputer** within the pipeline to handle null values using median and most-frequent strategies.

### **2. The Production Pipeline Architecture**
To ensure the project can be understood in one go, I used a **scikit-learn Pipeline** to bundle all steps:
*   **Numeric Transformer:** Applied **StandardScaler** to features like `tenure` and `MonthlyCharges` to ensure unit-variance.
*   **Categorical Transformer:** Applied **OneHotEncoder** to handle non-numeric data without manual intervention.
*   **Unified Model:** Combined the **ColumnTransformer** with a **RandomForestClassifier** into a single executable object.

---

## **📊 Performance Metrics (Final Results)**
The project focused on **Precision** and **Recall** to balance the cost of false alarms against the risk of missing a churning customer.

| Metric | Result (Class 1 - Churn) |
| :--- | :--- |
| **Accuracy** | **~79%**|
| **Precision** | **0.63**|
| **Recall** | **0.49** |
| **F1-Score** | **0.55** |

### **Visual Insights**
*   **The Churn Drivers:** The analysis reveals that **tenure** and **TotalCharges** are the top mathematical predictors of customer loyalty.
   <img width="1043" height="530" alt="Screenshot 2026-05-13 at 10 05 12 PM" src="https://github.com/user-attachments/assets/f18e3e9d-9e04-4e1d-b5aa-2b157197b94d" />

*   **Confusion Matrix:** Successfully identified **927** stable customers and **184** potential churners in the test set.
   <img width="651" height="549" alt="Screenshot 2026-05-13 at 10 05 33 PM" src="https://github.com/user-attachments/assets/35a9d414-f799-4e15-b0b4-9b8c5fd33f4f" />


---

## **⚙️ Configuration & Hyperparameters**
Following the **Industry Checklist**, the following parameters were identified via **GridSearchCV** (5-fold Cross-Validation) to provide the most stable model:
*   **Classifier:** RandomForestClassifier.
*   **max_depth:** 10.
*   **n_estimators:** 100.
*   **random_state:** 42.

---

## **🚀 Deployment & Running Instructions**

### **Option 1: Google Colab (Recommended)**
1.  Open the project notebook in **Google Colab**.
2.  Run the first cell; it will prompt you to upload the dataset.
3.  Upload **Telco-Customer-Churn.csv**.
4.  The pipeline will automatically handle cleaning, scaling, and generate the **Production Model File**.

### **Option 2: Production Inference**
The model is saved as **`best_churn_pipeline.joblib`**.
*   This file is a binary "container" that holds your scalers, encoders, and weights.
*   **To Run:** Use `joblib.load('best_churn_pipeline.joblib')` to make predictions on raw data instantly.

---

## **🧠 Lessons Learned**
*   **Automation over Manual Steps:** Using a **Pipeline** prevents the "it works on my machine" problem by ensuring preprocessing is identical in training and testing.
*   **Signal Identification:** I learned that while many features exist, the **Contract Type** and **Tenure** carry the most signal for business logic.
*   **Deployment Readiness:** A model isn't finished until it's exported. Saving the weights in a **.joblib** format is the bridge between research and a real-world application.

---

## **👨‍💻 Author**
**Shivi Srivastava**  
Aspiring AI Engineer | Amity University Uttar Pradesh
