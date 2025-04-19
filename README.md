**[![Open in Streamlit](https://img.shields.io/badge/Launch%20App-Streamlit-%23FF4B4B?logo=streamlit)](https://ml-healthcare-premium-prediction-7qrpw78zqct4zhdm7u8v2d.streamlit.app/)**  
# HealthCare Insurance Premium Prediction


### **Business Problem**
Insurance companies need to accurately predict a customer’s health risk to determine premium costs.

Inaccurate predictions can cause:

- Undercharging high-risk individuals, resulting in financial losses

- Overcharging low-risk individuals, leading to customer dissatisfaction and churn

The objective is to build a reliable model that provides accurate risk estimates and reduces extreme prediction errors, aligning with business goals.

###  **Objective**  
The goal of this project is to develop an accurate and reliable insurance risk prediction model that meets business requirements:  
 **Accuracy >95%** (R² ~0.95 or higher)  
 **Extreme error rate ≤10%**  

## **Feature Importance Analysis**  
#### **Most Important Features:**  
- **Insurance Plan** and **Age** have the strongest impact on predictions.  
- **Normalized Risk Score** and **BMI Category (Obesity)** also play significant roles.  

#### **Moderately Important Features:**  
- **Smoking Status (Regular, Occasional)** and **Employment Status (Self-Employed)** contribute but with smaller coefficients.  

#### **Least Important Features:**  
- **Marital Status (Unmarried), Number of Dependants, and Income Level** have minimal influence.  

---

## **Extreme Error Analysis & Model Segmentation Strategy**  
#### **Issue Identified:**  
- **Initial extreme error rate:** **30%** (far exceeding the acceptable threshold).  
- **Young Age Group (≤25) Without Genetic Factors:** **Extreme error rate: 73%** – a major performance issue.  
- **Young Age Group (≤25) With Genetic Factors:** **Extreme error rate: 2%** – significant improvement.  
- **Older Age Group (>25):** **Extreme error rate: 0.3%** – acceptable performance.  

#### **Solution Approach: Segmentation-Based Modeling**  
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

**XGBoost significantly outperformed Linear & Ridge Regression.**  
**Hyperparameter tuning improved accuracy to 99.7%.**  
**Extreme errors reduced to 0.3%, meeting business requirements.**  

---

### **Age Group: ≤25 ("Young") Without Genetic Factors**  

| Model                         | R² Score (Train/Test) | Extreme Errors (%) |
|--------------------------------|-----------------------|--------------------|
| Linear & Ridge Regression      | 0.602                 | -                  |
| XGBoost (Before Tuning)        | 0.603                 | -                  |
| XGBoost (After Tuning)         | 0.599                 | 73%                |

 **Extreme errors were too high (73%), failing business requirements.**  
 **R² was only ~60%, indicating poor model fit.**  
 **This approach was not viable, requiring additional features.**  

---

### **Age Group: ≤25 ("Young") With Genetic Factors**  

| Model                         | R² Score (Train/Test) | Extreme Errors (%) |
|--------------------------------|-----------------------|--------------------|
| Linear & Ridge Regression      | 0.988                 | -                  |
| XGBoost (Before Tuning)        | 0.987                 | -                  |
| XGBoost (After Tuning)         | 0.987                 | 2%                 |

 **Introducing genetic factor-based features significantly improved model accuracy.**  
 **Extreme errors reduced from 73% to 2%, now within the acceptable range.**  
**XGBoost performed best with fine-tuning, achieving ~98.7% accuracy.**  

---


### **Conclusion**

The insurance risk prediction model was developed using Linear Regression, Ridge Regression, and XGBoost, with a focus on meeting business requirements of >95% accuracy and <10% extreme errors.

### **Key Findings:**

- Feature Importance: Age and Insurance Plan had the most significant impact on predictions.

### **Segmentation Approach Improved Accuracy:**

- Older Age Group (>25): XGBoost (Tuned) performed exceptionally well with 99.7% accuracy and only 0.3% extreme errors.

- Young Age Group (≤25) Without Genetic Factors: The model struggled, achieving only 60% accuracy with 73% extreme errors, making it unsuitable.

- Young Age Group (≤25) With Genetic Factors: Accuracy improved to 98.7% with 2% extreme errors, making it an effective solution.

### **Final Decision:**

**A two-model segmentation approach is the best solution:**

- Use the XGBoost model (After Tuning) separately for age groups to ensure high accuracy and minimal errors.

- For young individuals (≤25), incorporate genetic factors to improve predictions.

- This strategy ensures the model meets business expectations, reducing risk while maintaining predictive accuracy.

