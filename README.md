# LoanTap Case Study: Building classification model to predict loan eligibility

## **Overview**
LoanTap is a fintech platform that delivers customized loan products to millennials, focusing on instant, flexible loans with consumer-friendly terms. This case study dives into the underwriting process for **Personal Loans**, with the goal of determining an individual’s creditworthiness and recommending appropriate repayment terms.

---

## **Problem Statement**
Given a set of attributes for an individual, determine:
1. Whether a credit line should be extended to them.
2. The recommended repayment terms.

---

## **Dataset**
The analysis uses the [LoanTapData.csv](https://drive.google.com/file/d/1ZPYj7CZCfxntE8p2Lze_4QO4MyEOy6_d/view?usp=sharing) dataset. Below is a brief description of key features:

| **Feature**               | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| `loan_amnt`              | Loan amount requested by the borrower.                                           |
| `term`                   | Loan repayment period in months (36 or 60).                                      |
| `int_rate`               | Interest rate applied to the loan.                                               |
| `installment`            | Monthly payment amount.                                                          |
| `grade`, `sub_grade`     | Loan grade assigned by LoanTap.                                                  |
| `emp_length`             | Employment length in years (0-10+).                                              | 
| `home_ownership`         | Borrower’s home ownership status.                                                |
| `annual_inc`             | Self-reported annual income.                                                     |
| `verification_status`    | Status of income verification.                                                   |
| `loan_status`            | Target variable indicating loan outcome.                                         |
| `dti`                    | Debt-to-income ratio.                                                            |
| `revol_util`             | Revolving line utilization rate.                                                 |
| `mort_acc`, `pub_rec`    | Number of mortgage accounts and public derogatory records.                       |

For a complete data dictionary, refer to the dataset.

---

## **Concepts Used**
- **Exploratory Data Analysis (EDA)**
- **Feature Engineering**
- **Logistic Regression Modeling**
- **Precision vs Recall Tradeoff**
- **Actionable Insights and Recommendations**

---

## **Steps Performed**

### **1. Exploratory Data Analysis**
- **Univariate Analysis**: Analyzed distributions of continuous and categorical variables.
- **Bivariate Analysis**: Explored relationships between features and the target variable.
- **Visualization Tools**: Used count plots, box plots, heatmaps, and pair plots to derive insights.

### **2. Feature Engineering**
- **Flags for Key Features**: Created binary flags for:
  - `pub_rec`: 1 if > 1, else 0.
  - `mort_acc`: 1 if > 1, else 0.
  - `pub_rec_bankruptcies`: 1 if > 1, else 0.
- **Handling Missing Values**: Imputed missing data using median/mode where applicable.
- **Feature Encoding**: Converted categorical variables to numeric using one-hot encoding.

### **3. Preprocessing**
- **Duplicate Removal**: Identified and removed duplicate records.
- **Unused Features**: Dropped irrelevant columns (e.g., `Address`, `title`).
- **Scaling**: Applied `StandardScaler` to normalize continuous variables.

### **4. Model Development**
- **Logistic Regression**: Built a logistic regression model to classify loan status.
- **Hyperparameter Tuning**: Optimized regularization parameters for improved performance.

### **5. Evaluation Metrics**
- **Confusion Matrix**: Analyzed true positives, false positives, true negatives, and false negatives.
- **Classification Report**: Evaluated precision, recall, F1-score, and accuracy.
- **AU-ROC Curve**: Visualized model’s discriminatory power.
- **Precision-Recall Curve**: Assessed trade-offs between precision and recall.

---

## **Results and Insights**

### **Model Performance**
| **Metric**         | **Value** |
|--------------------|-----------|
| Precision          | 81%       |
| Recall             | 98%       |
| Accuracy           | 80%       |
| F1 Score           | 88%       |
| ROC-AUC            | 71%       |


### Tradeoff Questions

1. **Minimizing False Positives**:  
   - Use precision as a key metric to reduce false positives.  
   - Implement cost-sensitive learning to weigh defaulters higher in the model.  
   - Utilize robust feature selection to focus on predictors highly indicative of defaults (e.g., DTI, credit history).  
   - Leverage ensemble methods (e.g., Random Forest, Gradient Boosting) to improve classification performance.

2. **Preventing NPAs (Non-Performing Assets)**:  
   - Prioritize recall to minimize missed defaulters (false negatives).  
   - Apply stricter approval thresholds and include early-warning indicators such as declining credit utilization or increasing debt.  
   - Regularly recalibrate the model with updated data to adapt to evolving borrower behavior.  
   - Include manual review for borderline cases flagged by the model.

---

### Actionable Insights & Recommendations

1. **Data Insights**: Focus on borrowers with high DTI, low sub-grades, or poor credit histories as they show higher default risks.  
2. **Model Improvements**: Implement explainable AI techniques to understand why loans are rejected, enabling transparent decision-making.  
3. **Operational Strategies**: Use segmentation (e.g., by purpose or employment length) to offer tailored products, enhancing loan approval while controlling risk.  
4. **Risk Mitigation**: Introduce dynamic credit limits and adjust interest rates based on individual risk profiles.  
5. **Continuous Monitoring**: Regularly monitor the model’s performance and update it with new data to capture trends
