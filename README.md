![Churn Analysis Banner](images/Cc%20Churn%20Banner.jpg)


## 📌 Project Overview
This project analyzes credit card customer churn across **10,127 accounts** (16.1% baseline churn rate) to identify early behavioral warning signs. Using `pandas`, `matplotlib`, `seaborn`, and `plotly`, the analysis moves away from static demographic profiling to highlight dynamic usage metrics — such as transaction drops, mid-tier spending patterns, low utilization ratios, and rising support calls — providing actionable insights for proactive retention strategies. No machine learning or feature engineering was used, per the project's defined scope; findings are drawn purely through EDA and visualisation.

## Guidance
- [ETL Notebook](jupyter_notebooks/ETL_ChurnAnalysis.ipynb)
- [Analysis & Visualisation Notebook](jupyter_notebooks/Analysis_Visualization.ipynb)
- [Conclusions Notebook](jupyter_notebooks/Conclusions.ipynb)
- [Raw Data](data/raw/BankChurners.csv)
- [Cleaned Data](data/cleaned/BankChurners_cleaned.csv)

## 📊 Dataset Content
Data comes from the [Credit Card Customers dataset on Kaggle](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers), containing 10,127 customer records across 23 columns, including demographic details, account activity, and churn status (`Attrition_Flag`).

## Business Requirements
A bank manager is concerned about rising customer churn in their credit card services. The goal is to identify which customers are likely to churn based on their behaviour, so the bank can take proactive steps to retain them, and to provide clear, actionable insight rather than a black-box prediction.


## 🧪 Hypotheses & Results

### Hypothesis 1: Demographic Impact (Gender & Income)
* **Hypothesis**: Demographics like gender and income strongly drive churn risk.
* **Result**: Gender shows minimal difference in churn counts. Income shows a weak, non-linear U-shaped relationship ($120K+ earners churn at 17.3%, but mid-income churns least), making demographics unreliable standalone predictors.

### Hypothesis 2: Transaction Activity & Frequency
* **Hypothesis**: Customers with fewer annual transactions and dropping activity levels are far more likely to churn.
* **Result**: **Supported**. Declining Transaction Count (r = -0.37) is the single strongest predictor. Churned customers average ~40% fewer transactions (median 43 vs 70/year).

### Hypothesis 3: Customer Activity Segmentation
* **Hypothesis**: Churn is highest among the lowest-spending customers.
* **Result**: **Partially Supported**. Churn heavily clusters in the mid-tier activity range (30–90 transactions, £1,000–£10,000 spend). High-activity customers (100+ transactions) show virtually zero churn.

### Hypothesis 4: Credit Line Engagement (Balance & Utilization)
* **Hypothesis**: Lower revolving balances and low card utilization precede account closures.
* **Result**: **Supported**. Attrited accounts maintain lower revolving balances (median ~1,300) and sit primarily at utilization ratios under 0.3.

### Hypothesis 5: Customer Friction vs. Time Inactive
* **Hypothesis**: Longer inactivity periods indicate churn better than customer service calls.
* **Result**: Inactive months are non-predictive (both groups sit at 2–3 months). Higher support contact count (r = +0.20, median 3 calls vs. 2) is a much stronger warning sign of customer frustration before exit.

## 🎨 The Rationale to Map Business Requirements to Data Visualisations
* **Pie Chart (Customer Churn Distribution)**: Establishes the 16.1% baseline churn rate to quantify overall revenue risk and justify retention spending.
* **Bar Chart (Churn by Gender)**: Compares attrition across genders to determine whether marketing should target a specific sex (shows negligible impact).
* **Interactive Horizontal Bar Chart (Income Category)**: Evaluates churn volume across income bands, revealing a U-shaped pattern where high earners ($120K+) churn at higher rates.
* **Correlation Heatmap & Top Factors Bar Plot**: Ranks all numeric variables by churn correlation, proving behavioral signals (r = -0.37) far outweigh demographics.
* **Transaction Count Box Plot**: Highlights the ~40% drop in transaction frequency (median 43 vs 70), setting an automated warning threshold at 50–55 transactions.
* **Transaction Count vs. Amount Scatter Plot**: Uncovers the high-risk mid-tier cluster (30–90 transactions, £1K–£10K spend) and confirms high-activity users (100+) rarely churn.
* **Revolving Balance & Utilization Box Plots**: Demonstrates that attrited accounts carry lower balances and low utilization (<0.3), framing a behavioral warning signal.
* **Months Inactive & Contacts Count Box Plots**: Disproves inactivity as a churn signal while establishing rising support calls as an active marker of customer frustration.

## 🛠️ Analysis Techniques & Methods
* **ETL Pipeline**: Data cleaning, "Unknown" value handling, duplicate checks, and irrelevant column removal in Jupyter Notebooks.
* **Exploratory Data Analysis (EDA)**: Univariate distributions, correlation matrix evaluation, and bivariate risk pattern isolation.
* **Visual Data Storytelling**: Combined static (matplotlib, seaborn) and interactive (plotly) charts to map business metrics to actionable risk profiles.

## ⚖️ Ethical Considerations & Data Privacy
Financial data is sensitive. `CLIENTNUM` was retained only as a unique account identifier and excluded from all analytical interpretation, holding no meaning of its own. "Unknown" values in `Education_Level`, `Marital_Status`, and `Income_Category` (7–15% of records each) were kept as a valid category rather than imputed, to avoid introducing assumptions not supported by the data.


## 🧰 Technologies Used
* **Environment**: VS Code, Jupyter Notebooks
* **Language**: Python
* **Data Manipulation**: pandas, numpy
* **Data Visualization**: matplotlib, seaborn, plotly
* **Version Control**: Git & GitHub

# Planning:
* I used a github [project board] (https://github.com/users/hemacbaker-byte/projects/2/views/1) to help me plan and keep track of my progress.


# Development Roadmap:
Had an issue with plotly chart, with the help of claude transported to the image as static for easy view.


## Credits
* [Code Institute](https://codeinstitute.net/) — Referred to LMS for charts maipulation and usage & template used for README.
* [Kaggle: sakshigoyal7](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers) — dataset source.
* Claude  — Used for debugging, story telling.
* Rory - Guided with Vs code commit.
* Vasi - Guided to improvise my project board.

## Media
Banner image created for this project using Gemini.

# Acknowledgements: 
Special thanks to my tutors Emma Lamont, Rory, Vasi, Marko from the Code Institute for all their help on the course!