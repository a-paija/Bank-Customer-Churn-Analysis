## 🟦 Project Background

Customer churn is a critical challenge for financial institutions, as retaining existing customers is significantly more cost-effective than acquiring new ones. Mavenland Bank has experienced elevated churn rates but lacks a structured, data-driven understanding of who is leaving, why they leave, and how to intervene effectively.

The dataset used in this project consists of **10,000 customer records**, combining demographic attributes, account behavior, and churn outcomes. However, due to inconsistencies in the raw data and lack of integrated analysis, the organization is unable to clearly identify churn drivers or implement targeted retention strategies.

Without structured analysis, Mavenland Bank is unable to answer key business questions such as:

- Which customer segments are most likely to churn  
- What behavioral or financial patterns signal churn risk  
- How churn risk varies across regions and demographics  
- Which customers should be prioritized for retention efforts  

**Overall Goal:**  
Reduce customer churn by **25% within two quarters** by identifying high-risk customers and enabling targeted, data-driven retention strategies.

This project bridges that gap by transforming raw customer data into actionable insights using **Python (Pandas, Scikit-learn)**, data visualization, and predictive modeling.

- Exploratory analysis highlights where churn risk is concentrated  
- Predictive modeling explains why customers churn and who is at risk  

Together, they enable both proactive intervention and strategic decision-making.

---

Targeted Python scripts and full analysis can be found [here](https://github.com/a-paija/Bank-Customer-Churn-Analysis/blob/main/Churn_Script.py)

An interactive Tableau Dashboard can be found [here](https://public.tableau.com/app/profile/ajin.paija/viz/CustomerChurnDashboard_17650248694380/Story1)

---

## 🟦 Business Objective and Data Structure

The primary objective of this analysis is to **predict customer churn and identify actionable retention opportunities** to stabilize revenue and improve customer lifetime value.

Specifically, this project aims to:

- Identify key drivers of customer churn  
- Segment customers based on churn risk  
- Evaluate churn patterns across demographics and regions  
- Build a predictive model to classify at-risk customers  
- Translate insights into targeted retention strategies  



## 🟦 Data Structure & Initial Checks

The dataset consists of **10,000 customer records with 13 features** spanning:

- **Demographics:** Age, Gender, Geography  
- **Financial Profile:** Credit Score, Balance, Estimated Salary  
- **Account Behavior:** Tenure, Number of Products, Activity Status  
- **Outcome Variable:** Churn (Exited)  

Data originated from multiple tables and required consolidation before analysis.



## 🟦 Data Cleaning (Python)

Before analysis, extensive data preparation was conducted to ensure accuracy and usability.

**Key steps included:**

- Standardizing numeric formats (currency → float)  
- Cleaning inconsistent categorical values (e.g., geography labels)  
- Handling missing values and removing duplicates  
- Merging customer and account datasets  
- Engineering new features (age groups, credit score segments)  

These steps ensured the dataset was suitable for both exploratory analysis and predictive modeling.



## 🟩 Executive Summary

Below is a screenshot of the Churn Demographics Dashboard Tableau Visualisations. The entire interactive Tableau Dashboard can be found [here](https://public.tableau.com/app/profile/ajin.paija/viz/CustomerChurnDashboard_17650248694380/Story1).

<img src="Images/Churn Demographics.png" alt="ChurnDemographics" width="750" height="850"/>


Mavenland Bank exhibits an overall churn rate of **20.37%**, meaning approximately **1 in 5 customers leave**, which is elevated relative to industry expectations.

However, churn is not evenly distributed—it is highly concentrated in specific customer segments:

- **Germany:** ~32% churn  
- **Other regions:** ~16% churn  
- **Customers aged 50–60:** ~56% churn  
- **Female customers:** 25% churn  
- **Male customers:** 16.5% churn  

Predictive modeling further reveals that churn is driven primarily by:

- Age  
- Number of products  
- Account balance  
- Estimated salary  

Most importantly, churn risk is **predictable and segmentable**:

- ~7% of customers are high-risk but represent high-value accounts  
- These customers tend to have higher balances and more products  

**Conclusion:**

The primary issue is not customer acquisition, but the bank’s inability to retain high-value, high-risk customers effectively.



## 🟨 Churn Trends & Customer Segmentation

Churn patterns reveal that customer attrition is structurally driven by demographic and behavioral factors rather than random occurrence.

- **Overall churn rate:** 20.4%  
- **High-risk segments:** >50% churn  
- **Low-risk segments:** <10% churn  

**Business Insight:**  
Churn is systematic and segment-driven, meaning targeted interventions outperform broad strategies.



## 🟨 Regional Performance Insights

Churn varies significantly across geographic regions:

- **Germany:** ~32% churn (highest risk)  
- **France & Spain:** ~16% churn  

**Business Insight:**  
Germany is a high-priority market requiring targeted retention strategies.



## 🟨 Demographic & Behavioral Drivers

Churn is strongly influenced by customer characteristics:

**Age:**
- 51–60: ~56% churn  
- 18–30: ~7.5% churn  

**Gender:**
- Female: ~25% churn  
- Male: ~16.5% churn  

**Credit Score:**
- Poor credit: ~22% churn  
- Good credit: ~18.6% churn  

**Business Insight:**  
Churn risk increases with age and financial exposure, requiring personalized retention strategies.



## 🟨 Predictive Modeling & Key Drivers

A **Random Forest model** was developed:

- **Accuracy:** 86.7%  
- **Precision:** 75.7%  
- **Recall:** 51.4%  

**Key predictors:**

- Age  
- Number of products  
- Balance  
- Estimated salary  

**Business Insight:**  
Churn can be predicted with high accuracy, though recall can be improved.



## 🟧 Customer Risk Segmentation

Customers were segmented into three risk tiers:

### High Risk (~7%)
- Age 45–65  
- High balances  
- Multiple products  

### Medium Risk (~10%)
- Moderate profiles  
- Early warning segment  

### Low Risk (~83%)
- Younger  
- Lower balances  
- Fewer products  

**Business Insight:**  
A small segment (~7%) represents disproportionate revenue risk.



## 🟥 Model Performance & Limitations

Limitations include:

- Imbalanced dataset (~20% churn)  
- Limited behavioral features  
- No hyperparameter tuning  

**Business Insight:**  
Even a baseline model provides actionable predictive power.



## 🟩 Strategic Recommendations & Actions

## 1. Target High-Risk, High-Value Customers
**Impact:** High  
- Prioritize customers aged 45+ with high balances  
- Assign relationship managers  
- Offer tailored incentives  

## 2. Focus on High-Churn Regions (Germany)
**Impact:** High  
- Investigate regional drivers  
- Implement localized strategies  

## 3. Develop Demographic-Specific Strategies
**Impact:** High  
- Address higher churn among female customers  
- Personalize engagement  

## 4. Improve Predictive Model Performance
**Impact:** Medium  
- Add behavioral data  
- Optimize model thresholds  

## 5. Build Proactive Retention Systems
**Impact:** High  
- Deploy early-warning systems  
- Automate retention workflows  



## 🟩 Final Summary

This project demonstrates a complete end-to-end churn analysis workflow:

- Data cleaning  
- Exploratory analysis  
- Predictive modeling  
- Segmentation  
- Strategic recommendations  

**Key Takeaway:**  
Customer churn is predictable, concentrated, and highly actionable with a structured, data-driven approach.

By focusing on high-risk, high-value customers, Mavenland Bank can significantly reduce churn, stabilize revenue, and improve long-term profitability.
