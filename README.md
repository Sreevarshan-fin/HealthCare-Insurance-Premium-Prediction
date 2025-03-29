# HealthCare-Insurance-Premium-Prediction

# HealthCare Insurance Risk Prediction & Model Optimization  

## **Objective**  
The goal of this project is to develop an accurate and reliable insurance risk prediction model that meets business requirements:  
✔ **Accuracy >95%** (R² ~0.95 or higher)  
✔ **Extreme error rate ≤10%**  

## **Feature Importance Analysis**  
### **Most Important Features:**  
- **Insurance Plan** and **Age** have the strongest impact on predictions.  
- **Normalized Risk Score** and **BMI Category (Obesity)** also play significant roles.  

### **Moderately Important Features:**  
- **Smoking Status (Regular, Occasional)** and **Employment Status (Self-Employed)** contribute but with smaller coefficients.  

### **Least Important Features:**  
- **Marital Status (Unmarried), Number of Dependants, and Income Level** have minimal influence.  

---

## **Extreme Error Analysis & Model Segmentation Strategy**  
### **Issue Identified:**  
- **Initial extreme error rate:** **30%** (far exceeding the acceptable threshold).  
- **Young Age Group (≤25) Without Genetic Factors:** **Extreme error rate: 73%** – a major performance issue.  
- **Young Age Group (≤25) With Genetic Factors:** **Extreme error rate: 2%** – significant improvement.  
- **Older Age Group (>25):** **Extreme error rate: 0.3%** – acceptable performance.  

### **Solution Approach: Segmentation-Based Modeling**  
- **Age Group >25 ("Rest")** – A dedicated model that meets business requirements.  
- **Age Group ≤25 ("Young") Without Genetic Factors** – Poor accuracy; requires a better approach.  
- **Age Group ≤25 ("Young") With Genetic Factors** – Introduced genetic factor-based features, improving performance significantly.  

---

## **Model Performance Comparison**  

### **Age Group: >25 ("Rest")**  

| Model                         | R² Score (Train/Test) | Extreme Errors (%) |
|--------------------------------|-----------------------|--------------------|
| Linear & Ridge Regression      | 0.953                 | -                  |
| XGBoost (Before Tuning)        | 0.994                 | -                  |
| XGBoost (After Tuning)         | 0.997                 | 0.3%               |

✔ **XGBoost significantly outperformed Linear & Ridge Regression.**  
✔ **Hyperparameter tuning improved accuracy to 99.7%.**  
✔ **Extreme errors reduced to 0.3%, meeting business requirements.**  

---

### **Age Group: ≤25 ("Young") Without Genetic Factors**  

| Model                         | R² Score (Train/Test) | Extreme Errors (%) |
|--------------------------------|-----------------------|--------------------|
| Linear & Ridge Regression      | 0.602                 | -                  |
| XGBoost (Before Tuning)        | 0.603                 | -                  |
| XGBoost (After Tuning)         | 0.599                 | 73%                |

🚨 **Extreme errors were too high (73%), failing business requirements.**  
🚨 **R² was only ~60%, indicating poor model fit.**  
🚨 **This approach was not viable, requiring additional features.**  

---

### **Age Group: ≤25 ("Young") With Genetic Factors**  

| Model                         | R² Score (Train/Test) | Extreme Errors (%) |
|--------------------------------|-----------------------|--------------------|
| Linear & Ridge Regression      | 0.988                 | -                  |
| XGBoost (Before Tuning)        | 0.987                 | -                  |
| XGBoost (After Tuning)         | 0.987                 | 2%                 |

✔ **Introducing genetic factor-based features significantly improved model accuracy.**  
✔ **Extreme errors reduced from 73% to 2%, now within the acceptable range.**  
✔ **XGBoost performed best with fine-tuning, achieving ~98.7% accuracy.**  

---

## **Final Conclusion & Recommendations**  
✔ **For Age >25 ("Rest")**, XGBoost (after tuning) meets business requirements with **99.7% accuracy** and **0.3% extreme errors**.  
✔ **For Age ≤25 ("Young") Without Genetic Factors**, the model failed to meet business requirements (**73% extreme errors**).  
✔ **For Age ≤25 ("Young") With Genetic Factors**, accuracy improved to **98.7%** and extreme errors were reduced to **2%**, meeting business goals.  
✔ **A two-model segmentation approach ensures both age groups achieve the required performance thresholds.**  
✔ **Final Recommendation:** XGBoost (with tuning) is the best model for both segments. 🚀  
