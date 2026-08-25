# Hospital Emergency Room Analytics

An end-to-end healthcare analytics project built around a **Hospital Emergency Room dataset**, combining **Power BI, SQL, Python, and Excel** to move from descriptive reporting to statistical analysis, machine learning, forecasting, and operational decision support.

The project begins with an interactive Power BI dashboard that answers the basic question of **"What happened?"** and then extends those insights using SQL, Python, and Excel to investigate **why patterns appear, whether they are statistically meaningful, what can be predicted, and where operational improvements can be made**.

---

## 📌 Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Project Objectives](#project-objectives)
- [Dataset](#dataset)
- [Analytical Workflow](#analytical-workflow)
- [Tools & Technologies](#tools--technologies)
- [Repository Structure](#repository-structure)
- [Power BI Dashboard](#1-power-bi-dashboard)
- [SQL Analysis](#2-sql-analysis)
- [Python Statistical & ML Analysis](#3-python-statistical--ml-analysis)
- [Excel Analysis](#4-excel-analysis)
- [Key Findings](#key-findings)
- [Business Insights & Recommendations](#business-insights--recommendations)
- [Data Quality & Limitations](#data-quality--limitations)
- [How to Explore the Project](#how-to-explore-the-project)
- [Skills Demonstrated](#skills-demonstrated)
- [License](#license)

---

## Project Overview

This project analyzes **9,216 emergency room visits recorded between April 2023 and October 2024**.

The original Power BI dashboard provides a descriptive view of ER activity through patient volume, wait times, satisfaction, referrals, admissions, demographics, and day/hour patterns.

The project then builds an analytical layer on top of the dashboard using:

- **SQL** for business-focused aggregation, ranking, and operational analysis
- **Python** for statistical hypothesis testing, predictive modeling, clustering, and forecasting
- **Excel** for data-quality auditing, department analysis, and staffing-gap visualization
- **Power BI** for interactive reporting and stakeholder-facing dashboards

The result is a complete analytics workflow that connects **reporting → diagnosis → prediction → operational decision-making**.

---

## Business Problem

Emergency departments need to balance patient demand, waiting times, staffing capacity, referrals, admissions, and patient experience.

A dashboard can show that a particular time period has longer waits or that one department receives more referrals. However, descriptive patterns alone do not establish whether those differences are statistically meaningful or whether they can be predicted reliably.

This project therefore asks a broader set of business questions:

1. **What is happening in the ER?**
2. **Are the observed patterns statistically significant?**
3. **Can patient outcomes be predicted from the available information?**
4. **Can patients be meaningfully segmented?**
5. **When and where does demand exceed service capacity?**
6. **What should hospital operations do differently?**

---

## Project Objectives

The project was designed to:

- Build and evaluate an interactive ER performance dashboard
- Analyze patient volume, waiting time, satisfaction, referrals, and admissions
- Assess the quality and reliability of the underlying data
- Investigate relationships between operational and demographic variables
- Test whether observed differences are statistically significant
- Evaluate whether admission, wait time, and satisfaction can be predicted
- Segment patients into meaningful groups
- Forecast near-term ER patient volume
- Identify specific day/hour staffing gaps
- Translate analytical findings into practical operational recommendations

---

## Dataset

The analysis uses a hospital emergency room patient-level dataset containing information such as:

- Patient ID: Unique identifier assigned to each patient.
- Patient name: Name of the patient.
- Gender: Patient’s gender.
- Age: Patient’s age.
- Admission date: Date the patient was admitted.
- Race: Patient’s racial background.
- Wait time: Time the patient waited for care.
- Department referral: Department to which the patient was referred.
- Admission status: Patient’s admission or discharge status.
- Patient satisfaction score: Patient’s rating of their care experience.
- Arrival time/day information: Time and day the patient arrived.
- Case Manager assignment: Case manager assigned to the patient.


The reporting period covers **April 2023 to October 2024**, with **9,216 patient visits**.

The dataset was also subjected to structural quality checks. The audit found:

- **0 duplicate Patient IDs**
- **0 age outliers**
- **0 wait-time outliers**
- **2,517 visits with a satisfaction score**
- **6,699 visits without a satisfaction score**
- **27.3% satisfaction survey response rate**

The low satisfaction-response rate is therefore an important limitation when interpreting the satisfaction KPI.

---

## Analytical Workflow

The project follows a layered analytics workflow:

```text
Raw ER Dataset
      │
      ▼
Data Preparation & Quality Checks
      │
      ├───────────────┐
      ▼               ▼
 Power BI           SQL
 Descriptive        Business
 Dashboard          Analysis
      │               │
      └───────┬───────┘
              ▼
          Python
   Statistical & ML Analysis
              │
      ┌───────┼────────┐
      ▼       ▼        ▼
 Statistics   ML    Forecasting
      │       │        │
      └───────┼────────┘
              ▼
           Excel
   Audit + Operational Analysis
              │
              ▼
    Business Recommendations
```

The workflow was deliberately designed so that different tools answer different types of questions rather than duplicating the same analysis.

---

## Tools & Technologies

| Area | Tools |
|---|---|
| Data Visualization | Power BI |
| Data Analysis | SQL, Python, Excel |
| Database | SQLite |
| Python Data Processing | pandas |
| Statistical Analysis | scipy.stats |
| Forecasting | statsmodels |
| Machine Learning | scikit-learn |
| Clustering | K-Means, PCA |
| Spreadsheet Analysis | Excel, openpyxl |
| Development Environment | Jupyter Notebook |
| Reporting | PDF / Power BI |

---

# 1. Power BI Dashboard

The Power BI dashboard is the starting point of the project and provides the descriptive reporting layer.

It contains four main views:

### Monthly View

Tracks monthly ER activity, including:

- Patient volume
- Average wait time
- Patient satisfaction
- Referrals
- Admission status
- Age distribution
- Gender
- Race
- Day/hour patient volume

<img width="1221" height="744" alt="image" src="https://github.com/user-attachments/assets/39d78fc6-febe-4698-8446-02d272da18f2" />


### Consolidated View

Provides the overall picture across the complete reporting period.

Key metrics include:

- **9,216 patient visits**
- **35.3-minute average wait time**
- **3,816 referred patients**
- Approximately **50/50 admission vs. non-admission split**
- **40.7%** of patients seen within the 30-minute target

<img width="1219" height="745" alt="image" src="https://github.com/user-attachments/assets/54eeaec8-0834-440e-a620-84083e24d508" />


### Patient Details

Provides a row-level view of individual visits, allowing users to filter and investigate patient-level information including:

- Patient ID
- Patient name
- Gender
- Age
- Admission date
- Race
- Wait time
- Department referral
- Admission status

The dashboard supports drill-down and audit-style exploration of all 9,216 visits.

<img width="1222" height="747" alt="image" src="https://github.com/user-attachments/assets/13ad784c-0074-4e11-8784-02eb4b6f56fe" />


### Key Takeaways

Summarizes the major descriptive patterns across the ER dataset and translates dashboard metrics into operational observations.

<img width="1204" height="714" alt="image" src="https://github.com/user-attachments/assets/71e68f37-70dc-457a-a317-c9a26436cc45" />


---

# 2. SQL Analysis

The SQL notebook extends the dashboard by using **SQLite-based analysis** to answer business questions that require grouping, aggregation, comparison, and ranking.

### Questions addressed

#### Satisfaction Survey Response

Investigates the proportion of visits with satisfaction scores and compares responders with non-responders.

#### Department Performance

Ranks departments based on:

- Patient volume
- Average wait time
- Average satisfaction
- Admission rate

#### Staffing Gap Analysis

Aggregates the percentage of patients missing the 30-minute wait-time target by:

- Day of week
- Time of day

This identifies specific periods where operational capacity appears weakest.

#### Case Manager Analysis

Compares outcomes between visits with and without Case Manager assignment.

The SQL notebook focuses on answering business questions through structured data aggregation rather than simply reproducing dashboard visuals.

---

# 3. Python Statistical & ML Analysis

The Python notebook provides the deeper analytical layer of the project.

### Statistical Testing

The analysis includes:

- Welch's t-test
- Chi-square tests
- One-way ANOVA
- Kruskal-Wallis test
- Pearson correlation
- Spearman correlation

These tests were used to distinguish genuine statistical relationships from patterns that may simply be random variation.

### Predictive Modeling

The project evaluates several machine learning approaches:

**Admission prediction**
- Logistic Regression
- Random Forest Classifier
- ROC-AUC evaluation

**Wait-time prediction**
- Linear Regression
- Random Forest Regressor
- MAE / RMSE / R² evaluation

**Patient satisfaction prediction**
- Random Forest Classifier
- Feature importance
- ROC-AUC evaluation

### Patient Segmentation

K-Means clustering with PCA visualization was used to identify patient segments.

A **4-cluster solution** produced distinct groups primarily differentiated by age and admission status.

### Forecasting

A **Holt-Winters exponential smoothing model** with weekly seasonality was used to forecast near-term ER patient volume.

The forecast estimated approximately **16.1 patients per day**, compared with a historical average of approximately **15.9 patients per day**, indicating broadly stable near-term volume.

---

# 4. Excel Analysis

The Excel workbook provides a practical, stakeholder-friendly analysis layer.

It contains:

### Data Quality Audit

A formula-driven audit covering:

- Duplicate Patient IDs
- Age outliers
- Wait-time outliers
- Satisfaction response coverage
- Survey response rate

### Department Analysis

A department-level ranking comparing:

- Patient volume
- Average wait time
- Average satisfaction
- Admission rate

### Staffing Gap Heatmap

A conditional-formatted day × hour heatmap showing the percentage of visits missing the 30-minute target.

This makes the staffing analysis easy to interpret without requiring Python or SQL.

---

## Key Findings

### 1. ER volume is substantial but relatively stable

The dataset contains **9,216 visits across 19 months**, averaging approximately **485 visits per month**.

The 30-day Holt-Winters forecast projects approximately **16.1 patients per day**, very close to the historical average of approximately **15.9 patients per day**.

This does not indicate a need for an overall staffing-budget increase based on volume alone.

### 2. The 30-minute wait-time target is being missed frequently

Only **40.7%** of visits were completed within the 30-minute target, meaning **59.3% missed the target**.

This makes patient flow and staffing an important operational concern.

### 3. Satisfaction data has a major coverage limitation

Only **27.3% of visits have a recorded satisfaction score**.

Formal testing did not find significant differences between responders and non-responders in wait time or admission status, but the low response rate itself means the satisfaction KPI should be interpreted cautiously.

### 4. No statistically significant race-based wait-time disparity was detected

ANOVA and Kruskal-Wallis tests both failed to reject the null hypothesis:

- ANOVA: **p = 0.771**
- Kruskal-Wallis: **p = 0.775**

The observed differences in average wait time across race groups therefore do not provide statistical evidence of a race-based disparity in this dataset.

### 5. Wait time does not meaningfully explain satisfaction

The relationship between wait time and satisfaction was very weak:

- Pearson correlation: **r ≈ -0.02**
- **p ≈ 0.29**

This suggests that reducing wait time alone may not explain or substantially improve satisfaction scores in this dataset.

### 6. Department-level wait-time differences are relatively small

Neurology had the highest average wait time at **36.8 minutes**, followed by Physiotherapy at **36.6 minutes** and Gastroenterology at **35.8 minutes**.

However, the overall spread between departments was only around two minutes, suggesting that department-level differences are less important than the time-of-day staffing pattern.

### 7. Admission is not strongly explained by the available demographic variables

Chi-square tests found no significant relationship between admission and:

- Age group: **p = 0.882**
- Department referral: **p = 0.937**

The approximately 50% admission rate remains relatively consistent across these groups.

### 8. The available variables are poor predictors of admission and wait time

Both admission classification models produced ROC-AUC values close to **0.50**, while wait-time regression models produced R² values near zero.

The analysis therefore suggests that additional clinical variables such as **triage acuity, chief complaint, vital signs, and live queue length** would be needed to build more useful predictive models.

### 9. Patient segmentation is more promising than outcome prediction

K-Means clustering produced four distinguishable patient segments, primarily driven by **age and admission status**.

This provides a potential basis for age-appropriate communication or care-pathway design, although it is not a strong tool for predicting wait times.

### 10. The clearest operational signal is the staffing gap by time of day

The strongest staffing gaps occur during late-night and overnight periods.

The three highest-risk windows identified were:

- **Thursday 22:00–24:00:** 70.7% missed the target
- **Saturday 22:00–24:00:** 69.3%
- **Monday 02:00–04:00:** 68.5%

The Excel heatmap provides a direct way to translate these patterns into shift-level staffing decisions.

---

## Business Insights & Recommendations

Based on the analysis, the project points toward several practical actions.

### Shift staffing rather than increasing total staffing

Overall patient volume is relatively stable, so staffing changes should focus on **when staff are scheduled**, rather than simply increasing the overall staffing budget.

Late-night and overnight periods should receive particular attention.

### Improve satisfaction data collection

With only **27.3% survey coverage**, satisfaction should not be treated as a complete representation of patient experience.

Increasing response coverage would make the KPI substantially more useful for management decisions.

### Capture better clinical features

The predictive models demonstrate an important limitation of the current dataset.

For admission and wait-time prediction, future data collection should consider variables such as:

- Triage acuity
- Chief complaint
- Vital signs
- Queue length
- Current department capacity
- Staffing levels

### Treat statistical non-findings as useful findings

The analysis deliberately avoids forcing a relationship where the data does not support one.

The absence of significant relationships is itself useful because it prevents management from allocating resources based on misleading correlations.

### Evaluate Case Manager coverage through a better-designed pilot

Only approximately **5.2% of visits** had a Case Manager assigned.

The observed wait-time difference was not statistically significant, so the current data does not establish that Case Manager assignment improves outcomes.

A larger and more deliberately targeted pilot would provide stronger evidence.

---

## Data Quality & Limitations

The structural quality audit found:

- No duplicate Patient IDs
- No impossible ages
- No wait-time outliers outside the defined validation range

However, several analytical limitations remain.

### Satisfaction response rate

Only 27.3% of visits have satisfaction scores. Although the analysis did not detect significant bias in wait time or admission status between responders and non-responders, the response rate itself is a major limitation.

### Limited clinical variables

The dataset does not contain several variables that would normally be important for ER prediction, including triage acuity, chief complaint, vital signs, and live queue length.

This helps explain why the predictive models performed close to chance.

### Observational analysis

The findings describe relationships within the available dataset. They should not automatically be interpreted as causal relationships.

### Staffing analysis

The staffing heatmap identifies periods where the 30-minute target is frequently missed. It is best interpreted as a capacity signal and starting point for operational investigation, rather than proof that staffing alone caused the delays.

---

## How to Explore the Project

A recommended order for exploring the repository is:

### Step 1: Start with the Power BI dashboard

Open:

`1. Power BI Dashboard/Hospital ER Analysis.pbix`

This gives the overall business context and shows the original descriptive analysis.

### Step 2: Review the dashboard PDF

Open:

`1. Power BI Dashboard/Hospital ER Analysis .pdf`

This provides a static version of the dashboard without requiring Power BI.

### Step 3: Explore the SQL layer

Open:

`2. SQL & Python Notebooks/A. SQL_Business_Analysis.ipynb`

Focus on the department analysis, staffing-gap analysis, survey response analysis, and Case Manager analysis.

### Step 4: Explore the Python layer

Open:

`2. SQL & Python Notebooks/B. Python_Statistical_and_ML_Analysis.ipynb`

This contains the statistical tests, predictive models, clustering, and forecasting.

### Step 5: Review the Excel analysis

Open:

`3. Excel Workbook/Hospital_ER_Analysis.xlsx`

This provides the data-quality audit, department analysis, and staffing heatmap in a stakeholder-friendly spreadsheet format.

### Step 6: Review the business Q&A

Open:

`0. Data & Business Q&A/Hospital_ER_Analysis_Report_Business Q&A.pdf`

This brings the project together through the 26 business questions and their computed answers.

---

## Repository Structure

```text
Hospital-ER-Analytics/
│
├── 0. Data & Business Q&A/
│   ├── Hospital ER_Data.csv
│   └── Hospital_ER_Analysis_Report_Business Q&A.pdf
│
├── 1. Power BI Dashboard/
│   ├── Hospital ER Analysis .pdf
│   └── Hospital ER Analysis.pbix
│
├── 2. SQL & Python Notebooks/
│   ├── A. SQL_Business_Analysis.ipynb
│   └── B. Python_Statistical_and_ML_Analysis.ipynb
│
├── 3. Excel Workbook/
│   ├── Hospital_ER_Analysis.pdf
│   └── Hospital_ER_Analysis.xlsx
│
├── LICENSE
└── README.md
```

---

## Skills Demonstrated

### Data Analytics

- Exploratory Data Analysis
- Data Cleaning
- Data Validation
- Data Quality Auditing
- KPI Analysis
- Business Question Development
- Descriptive Analytics

### Business Analysis

- Translating business problems into analytical questions
- Diagnostic analysis
- Operational performance analysis
- Capacity planning
- Staffing analysis
- Business recommendations
- Decision-support reporting

### SQL

- SQLite
- Filtering and aggregation
- Grouped analysis
- Ranking
- Conditional logic
- Business-oriented analytical queries

### Python

- pandas
- scipy
- statsmodels
- scikit-learn
- Statistical hypothesis testing
- Correlation analysis
- Classification
- Regression
- Random Forest
- K-Means clustering
- PCA
- Time-series forecasting

### Data Visualization

- Power BI dashboards
- KPI cards
- Trend analysis
- Heatmaps
- Conditional formatting
- Excel charts
- Dashboard storytelling

### Analytical Thinking

- Separating signal from noise
- Interpreting statistical significance
- Evaluating model limitations
- Identifying data gaps
- Translating analytical results into operational actions

---

## Final Takeaway

The central finding of this project is not that every variable predicts every outcome.

It is that **the data was tested rigorously enough to determine where meaningful signal exists and where it does not**.

Most demographic, departmental, and operational variables did not provide strong predictive power for admission, wait time, or satisfaction. In contrast, **time-of-day and day-of-week patterns showed a clear operational signal**, while the low satisfaction survey response rate emerged as an important data-quality issue.

That distinction turns the project from a dashboard exercise into a broader **decision-support and analytical reasoning case study**.

---

## License

This project is available under the license included in the repository.
