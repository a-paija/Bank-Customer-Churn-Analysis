## 🟦 Project Background

Customer churn is a major revenue loss for financial institutions, as retaining existing customers is significantly more cost-effective than acquiring new ones. Mavenland Bank has experienced elevated churn rates but lacks a structured, data-driven understanding of who is leaving, why they leave, and how to intervene effectively.

Due to lack of integrated analysis, Mavenland Bank is unable to clearly identify churn drivers or implement targeted retention strategies. This project addresses that problem by using customer data (10,000 records across demographics, financials, and behavior) to **predict and prevent churn before it happens**.

This project addresses business questions such as:

- Which customer segments are most likely to churn  
- What behavioral or financial patterns signal churn risk  
- How churn risk varies across regions and demographics  
- Which customers should be prioritized for retention efforts  

**Overall Goal:**  
Reduce customer churn by **25% within two quarters** by identifying high-risk customers and enabling targeted, data-driven retention strategies.

This project transforms raw customer data into actionable insights using **Python (Pandas, Scikit-learn)**, Tableau data visualizations, and predictive modeling.

- Exploratory analysis highlights where churn risk is concentrated  
- Predictive modeling explains why customers churn and who is at risk  

---

Targeted Python scripts and full analysis can be found [here](https://github.com/a-paija/Bank-Customer-Churn-Analysis/blob/main/Churn_Script.py)

An interactive Tableau Dashboard can be found [here](https://public.tableau.com/app/profile/ajin.paija/viz/CustomerChurnDashboard_17650248694380/Story1)

---

## 🟦 Business Objective & Data Overview

The objective of this analysis is to create a model that can **predict customer churn and enable targeted retention strategies** to reduce revenue loss and improve customer lifetime value.

The analysis uses **10,000 customer records across 13 features**, including:

- Demographics (Age, Gender, Geography)  
- Financial attributes (Credit Score, Balance, Estimated Salary)  
- Account behavior (Tenure, Product count, Activity status)  
- Outcome variable: **Churn (Exited)**  

Raw data was consolidated and prepared to ensure reliability for analysis and modeling:

- Resolved inconsistencies in numeric and categorical fields  
- Removed duplicates and handled missing values  
- Merged customer and account-level data  
- Engineered key features (e.g., age groups, credit segments)  

Result: a **clean, structured dataset ready for analysis and predictive modeling**.



## 🟩 Executive Summary

Below is a screenshot of the Churn Demographics Dashboard Tableau Visualisations. The entire interactive Tableau Dashboard can be found [here](https://public.tableau.com/app/profile/ajin.paija/viz/CustomerChurnDashboard_17650248694380/Story1).

<img src="Images/Churn Demo.png" alt="ChurnDemographics" width="700" height="750"/>

Mavenland Bank exhibits an overall churn rate of **20.37%**, meaning approximately **1 in 5 customers leave**, which is elevated relative to industry expectations.

However, churn is not evenly distributed, it is highly concentrated in specific customer segments:

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

<details>
<summary>🟩 View Codes & Additional Graphs</summary>

```python
overall_churn = df['Exited'].mean()
print(f"Overall churn rate: {overall_churn:.2%}")
```
Calculates overall churn percentage.

<img src="Images/Churn Rate by Geography.png" alt="Geography" width="550" height="650"/>

```python
geo_churn = df.groupby('Geography')['Exited'].mean().reset_index()
plt.figure(figsize=(8, 6))
sns.barplot(x='Geography', y='Exited', data=geo_churn, palette="viridis")
plt.gca().yaxis.set_major_formatter(
    plt.FuncFormatter(lambda y, _: f'{y*100:.1f}%'))
plt.ylim(0, 0.4)
plt.title("Churn Rate by Geography", fontsize=14)
plt.ylabel("Churn Rate (%)", fontsize=12)
plt.xlabel("Geography", fontsize=12)
for i, row in geo_churn.iterrows():
    plt.text(i, row['Exited'] + 0.01,
             f"{row['Exited']*100:.1f}%", ha='center', fontweight='bold')
plt.show()
```
Compares churn rates across geographic regions.

<img src="Images/Churn Rate by Gender.png" alt="Gender" width="550" height="650"/>

```python
gender_churn = df.groupby('Gender')['Exited'].mean().reset_index()
plt.figure(figsize=(8, 6))
sns.barplot(x='Gender', y='Exited', data=gender_churn, palette="viridis")
plt.gca().yaxis.set_major_formatter(
    plt.FuncFormatter(lambda y, _: f'{y*100:.1f}%'))
plt.ylim(0, 0.30)
plt.title("Churn Rate by Gender", fontsize=14)
plt.ylabel("Churn Rate (%)", fontsize=12)
plt.xlabel("Gender", fontsize=12)
for i, row in gender_churn.iterrows():
    plt.text(i, row['Exited'] + 0.01,
             f"{row['Exited']*100:.1f}%", ha='center', fontweight='bold')
plt.show()
```
Analyzes churn differences by gender.

<img src="Images/Churn Rate by Age Group.png" alt="Age" width="550" height="650"/>

```python
age_bins = pd.cut(df['Age'], bins=[18, 30, 40, 50, 60, 70],
                  labels=['18–30', '31–40', '41–50', '51–60', '61–70'])
age_churn = df.groupby(age_bins)['Exited'].mean().reset_index()
age_churn.columns = ['Age Group', 'Exited']
plt.figure(figsize=(8, 6))
sns.barplot(x='Age Group', y='Exited', data=age_churn, palette="viridis")
plt.gca().yaxis.set_major_formatter(
    plt.FuncFormatter(lambda y, _: f'{y*100:.1f}%'))
plt.ylim(0, 0.65)
plt.title("Churn Rate by Age Group", fontsize=14)
plt.ylabel("Churn Rate (%)", fontsize=12)
plt.xlabel("Age Group", fontsize=12)
for i, row in age_churn.iterrows():
    plt.text(i, row['Exited'] + 0.02,
             f"{row['Exited']*100:.1f}%", ha='center', fontweight='bold')
plt.show()
```
Shows churn variation across age groups.

<img src="Images/Churn Rate by Credit Score Group.png" alt="Credit Score" width="550" height="650"/>

```python
credit_bins = [300, 579, 669, 739, 850]
credit_labels = ['Poor', 'Fair', 'Good', 'Excellent']
df['CreditScoreGroup'] = pd.cut(
    df['CreditScore'], bins=credit_bins, labels=credit_labels)
credit_churn = df.groupby('CreditScoreGroup')['Exited'].agg(
    ['count', 'mean']).reset_index()
credit_churn.columns = ['CreditScoreGroup', 'CustomerCount', 'ChurnRate']
plt.figure(figsize=(8, 6))
sns.barplot(x='CreditScoreGroup', y='ChurnRate', data=credit_churn,
            order=credit_labels, palette="viridis")
plt.gca().yaxis.set_major_formatter(
    plt.FuncFormatter(lambda y, _: f'{y*100:.1f}%'))
plt.ylim(0.16, 0.23)
plt.title("Churn Rate by Credit Score Group", fontsize=14)
plt.ylabel("Churn Rate (%)", fontsize=12)
plt.xlabel("Credit Score Group", fontsize=12)
for i, row in credit_churn.iterrows():
    plt.text(i, row['ChurnRate'] + 0.005,
             f"{row['ChurnRate']*100:.1f}%", ha='center', fontweight='bold')
plt.show()
```
Evaluates churn by credit score segments.

</details>

## 🟨 Predictive Modeling & Key Drivers

A **Random Forest classification model** was developed to predict whether a customer is likely to churn.

**Purpose of the Model:**  
The goal of this model is not just accuracy, but **actionability**, identifying *which customers are at risk before they leave*, so the bank can intervene proactively rather than reactively.

### Key Predictors of Churn

<img src="Images/Top Drivers of Customer Churn.png" alt="Drivers" width="700" height="750"/>


The model identifies the following as the most influential drivers:

- **Age** → Older customers show significantly higher churn rates  
- **Number of Products** → Customers with more products are at higher risk (potential dissatisfaction or complexity)  
- **Balance** → Higher balances correlate with increased churn risk (high-value customers leaving)  
- **Estimated Salary** → Higher-income customers are more likely to churn, likely due to more alternatives  

### Business Interpretation

- Churn is **predictable and not random**  
- High-value customers (high balance + salary) are disproportionately at risk  
- The model enables **targeted retention strategies**, rather than broad, inefficient campaigns  

### How This Model Can Be Used

- **Proactive Retention Campaigns**  
  → Flag at-risk customers before churn occurs  

- **Resource Allocation**  
  → Focus retention budgets on customers most likely to leave  

- **Personalization**  
  → Tailor offers based on risk profile and key drivers  

- **Early Warning System**  
  → Integrate into CRM systems for real-time churn monitoring

**Accuracy: 86.7%**  
  → The model correctly predicts churn vs. non-churn in ~87% of cases overall.  
  → However, accuracy alone can be misleading due to class imbalance (most customers do not churn).

**Precision: 75.7%**  
  → Of all customers predicted to churn, ~76% actually churned.  
  → This reflects how **reliable the model’s positive predictions are** (important for avoiding wasted retention efforts).

</details> 
<details> 
<summary>🟩 View Code</summary>

<img src="Images/Top Drivers of Customer Churn.png" alt="Churn Drivers" width="550" height="650"/>

```python
features = ['CreditScore', 'Geography', 'Gender', 'Age', 'Tenure', 'Balance',
            'NumOfProducts', 'HasCrCard', 'IsActiveMember', 'EstimatedSalary']
X = pd.get_dummies(df[features], drop_first=True)
y = df['Exited']
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, stratify=y, random_state=42)

rf_model = RandomForestClassifier(
    n_estimators=300, min_samples_split=5, random_state=42)
rf_model.fit(X_train, y_train)
rf_preds = rf_model.predict(X_test)

print("Random Forest Accuracy:", accuracy_score(y_test, rf_preds))
print(classification_report(y_test, rf_preds))
```
Builds and evaluates the churn prediction model.

```python
rf_importance = pd.DataFrame({
    'Feature': X.columns,
    'Importance': rf_model.feature_importances_ * 100
}).sort_values('Importance', ascending=False)

plt.figure(figsize=(10, 6))
sns.barplot(data=rf_importance.head(10), x='Importance',
            y='Feature', palette="viridis")
plt.title("Top Drivers of Customer Churn", fontsize=14)
plt.xlabel("Relative Impact on Churn (%)", fontsize=12)
plt.ylabel("Customer Attribute", fontsize=12)
plt.tight_layout()
plt.show()
```
Identifies key drivers influencing churn.

</details>

## 🟧 Customer Risk Segmentation

Customers were segmented into **three actionable churn risk tiers** based on predicted probabilities.

### Risk Definition

| Risk Level   | Probability Range | % of Customers |
|--------------|------------------|----------------|
| Low       | 0.00 – 0.40       | ~83%           |
| Medium    | 0.40 – 0.70       | ~10%           |
| High      | 0.70 – 1.00       | ~7%            |

### Segment Profiles & Interpretation

| Segment | Key Characteristics | Business Interpretation |
|--------|--------------------|--------------------------|
| High Risk | Age 45–65, high balances, multiple products | High-value customers most likely to churn → **largest revenue risk** |
| Medium Risk | Moderate balances, moderate engagement | **Early warning segment** → risk of escalation without intervention |
| Low Risk | Younger, lower balances, fewer products | Stable base → **low immediate churn risk** |

### Recommended Actions

| Segment | Strategy | Tactics |
|--------|----------|----------|
| High Risk | Immediate retention | Dedicated account managers, personalized offers, incentives |
| Medium Risk | Prevent churn | Targeted campaigns, engagement strategies |
| Low Risk | Maintain & grow | Low-cost engagement, upsell opportunities |


### Business Insight

A small portion of customers (**~7%**) represents **disproportionate financial risk**, meaning:

→ Retention efforts can be **highly focused and cost-efficient**  
→ Even small improvements in this segment can yield **significant revenue impact**

<details> 
<summary>🟩 View Code</summary>

```python
results = X_test.copy()

results['Actual'] = y_test.values
results['Churn_Prob'] = rf_model.predict_proba(X_test)[:, 1]
results['Prediction'] = rf_model.predict(X_test)

results['Risk_Tier'] = pd.cut(
    results['Churn_Prob'],
    bins=[-0.001, 0.40, 0.70, 1.001],
    labels=['Low Risk', 'Medium Risk', 'High Risk'],
    include_lowest=True
)
```
Assigns customers into churn risk tiers.

```python
risk_counts = results['Risk_Tier'].value_counts().sort_index()
print(risk_counts)

risk_stats = results.groupby('Risk_Tier')[
    ['Age', 'Balance', 'NumOfProducts', 'EstimatedSalary']].mean().round(2)
print(risk_stats)
```
Summarizes customer profiles by risk segment.

</details>

## 🟩 Strategic Recommendations & Action Plan

Recommendations are prioritized based on **expected revenue impact** and **feasibility**, directly tied to model insights.

| Initiative | Target Segment |  Objective |  Action | Impact |
|------------|----------------|--------------------|-------------|-----------------|
| Retain High-Value, High-Risk Customers | High Risk (Age 45+, high balance, multi-product) | Prevent immediate revenue loss | Assign relationship managers, deploy personalized incentives, proactive outreach | Protects largest revenue at risk; highest ROI retention effort |
| Address Regional Churn Concentration | Germany region | Reduce geographically concentrated churn | Conduct root-cause analysis (pricing, competition, service), implement localized campaigns | Reduces systemic churn drivers in high-risk market |
| Deploy Proactive Retention System | Medium → High Risk pipeline | Prevent churn escalation | Build early-warning triggers, automate CRM outreach, lifecycle-based engagement | Converts at-risk customers before churn occurs |
| Personalize Demographic Strategies | Female customer segment | Improve engagement & retention equity | Tailor messaging, offers, and product positioning based on behavioral insights | Closes segment-specific churn gaps |
| Enhance Predictive Model | All segments | Improve targeting accuracy | Incorporate behavioral data (transactions, engagement), optimize thresholds, retrain model | Increases precision of retention spend over time |
