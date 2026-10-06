```markdown
![Churn Analysis Banner](images/Cc%20Churn%20Banner.jpg)


## 📌 Project Overview
This project analyzes credit card customer churn across **10,127 accounts** (16.1% baseline churn rate) to identify early behavioral warning signs. Using `pandas`, `matplotlib`, `seaborn`, `plotly`, `scipy`, and `scikit-learn`, the analysis combines exploratory analysis, statistical hypothesis testing, and predictive modelling — moving from static demographic profiling to a validated, actionable churn risk model for proactive retention strategies.

## Guidance
- [ETL Notebook](jupyter_notebooks/01_ETL_ChurnAnalysis.ipynb)
- [Analysis & Visualisation Notebook](jupyter_notebooks/02_Analysis_Visualization.ipynb)
- [Conclusions Notebook](jupyter_notebooks/04_Conclusion.ipynb)
- [Statistical Analysis & Predictive Model Notebook](jupyter_notebooks/03_Statistical_ML_Analysis.ipynb)
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

### Hypothesis 6: Transaction Activity Is Statistically Significant
* **Hypothesis**: The difference in transaction count between churned and active customers is statistically significant, not due to random chance.
* **Result**: **Supported**. A two-sample t-test confirmed the gap is statistically significant (p < 0.05), formally validating the earlier visual and correlation findings.

### Hypothesis 7: Churn Can Be Predicted from Behavioural Data
* **Hypothesis**: A machine learning model trained on behavioural and account features can reliably identify customers likely to churn.
* **Result**: **Supported**. A logistic regression model achieved 83% accuracy and 78% recall on churned customers, correctly identifying roughly 3 in 4 at-risk accounts — demonstrating that churn is genuinely predictable from transaction activity, utilization, balance, and contact frequency, not demographic traits.

## 🎨 The Rationale to Map Business Requirements to Data Visualisations
* **Pie Chart (Customer Churn Distribution)**: Establishes the 16.1% baseline churn rate to quantify overall revenue risk and justify retention spending.
* **Bar Chart (Churn by Gender)**: Compares attrition across genders to determine whether marketing should target a specific sex (shows negligible impact).
* **Interactive Horizontal Bar Chart (Income Category)**: Evaluates churn volume across income bands, revealing a U-shaped pattern where high earners ($120K+) churn at higher rates.
* **Correlation Heatmap & Top Factors Bar Plot**: Ranks all numeric variables by churn correlation, proving behavioral signals (r = -0.37) far outweigh demographics.
* **Transaction Count Box Plot**: Highlights the ~40% drop in transaction frequency (median 43 vs 70), setting an automated warning threshold at 50–55 transactions.
* **Transaction Count vs. Amount Scatter Plot**: Uncovers the high-risk mid-tier cluster (30–90 transactions, £1K–£10K spend) and confirms high-activity users (100+) rarely churn.
* **Revolving Balance & Utilization Box Plots**: Demonstrates that attrited accounts carry lower balances and low utilization (<0.3), framing a behavioral warning signal.
* **Months Inactive & Contacts Count Box Plots**: Disproves inactivity as a churn signal while establishing rising support calls as an active marker of customer frustration.
* **Confusion Matrix**: Visualises the logistic regression model's prediction accuracy, distinguishing correctly identified churned/active customers from misclassifications.

## 📈 Statistical Analysis
Core statistical concepts (mean, median, standard deviation, probability distribution, hypothesis testing) are explained and applied directly to the data. A two-sample t-test confirmed that the gap in transaction count between churned and active customers is statistically significant (p < 0.05), validating the earlier visual finding with formal evidence.

## 🤖 Predictive Model
A logistic regression model was built using scikit-learn to estimate churn probability, chosen for its interpretability over black-box alternatives like random forests — producing clear probability scores a manager can act on directly. `class_weight='balanced'` was used to address the 16%/84% churn imbalance without manually resampling the data.

**Model Performance:** 83% overall accuracy, 78% recall on churned customers — correctly identifying roughly 3 in 4 at-risk accounts. Recall was prioritised over precision, since missing an at-risk customer is costlier to the bank than an unnecessary retention offer to a loyal one.

## 🎯 Customer Segmentation
Customers were segmented into Low, Medium, and High risk groups based on transaction activity and utilization ratio, allowing the bank to prioritise retention efforts by risk tier rather than treating all customers equally.

## 💡 Prototype: Interactive Retention Tool
Based on identified churn drivers, a proposed prototype is an internal dashboard where staff input a customer's key metrics (transaction count, utilization, contact frequency) to receive an instant churn risk score, enabling proactive, targeted retention outreach rather than reactive account review.

## 🛠️ Analysis Techniques & Methods
* **ETL Pipeline**: Data cleaning, "Unknown" value handling, duplicate checks, and irrelevant column removal in Jupyter Notebooks.
* **Exploratory Data Analysis (EDA)**: Univariate distributions, correlation matrix evaluation, and bivariate risk pattern isolation.
* **Statistical Testing**: Hypothesis testing (two-sample t-test) to validate observed differences between churned and active customers.
* **Predictive Modelling**: Logistic regression classification using scikit-learn, with train/test split and class-imbalance handling.
* **Visual Data Storytelling**: Combined static (matplotlib, seaborn) and interactive (plotly) charts to map business metrics to actionable risk profiles.

## ⚖️ Ethical Considerations & Data Privacy
Financial data is sensitive. `CLIENTNUM` was retained only as a unique account identifier and excluded from all analytical interpretation, holding no meaning of its own. "Unknown" values in `Education_Level`, `Marital_Status`, and `Income_Category` (7–15% of records each) were kept as a valid category rather than imputed, to avoid introducing assumptions not supported by the data.

## 🧰 Technologies Used
* **Environment**: VS Code, Jupyter Notebooks
* **Language**: Python
* **Data Manipulation**: pandas, numpy
* **Data Visualization**: matplotlib, seaborn, plotly
* **Statistics & Machine Learning**: scipy, scikit-learn
* **Version Control**: Git & GitHub

# Planning:
* I used a github [project board](https://github.com/users/hemacbaker-byte/projects/2/views/1) to help me plan and keep track of my progress.


# Development Roadmap:
Had an issue with plotly chart, with the help of claude transported to the image as static for easy view.

## 🔄 Reflection: Learning Journey
This project extended an initial EDA-only analysis into a full predictive pipeline, requiring new skills in statistical hypothesis testing and scikit-learn model building. The main challenge was correctly handling class imbalance in the churn target — addressed through `class_weight='balanced'` rather than manual oversampling, keeping the approach transparent and reproducible. This experience directly mirrors real-world data analyst work: moving from descriptive insight to predictive, actionable tooling for business stakeholders.

## Credits
* [Code Institute](https://codeinstitute.net/) — Referred to LMS for charts maipulation and Pandas & template used for README.
* [Kaggle: sakshigoyal7](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers) — dataset source.
* Claude - Used for debugging, story telling, Plotly, statistical analysis, and predictive modelling guidance.
* Rory - Guided with Vs code commit.
* Vasi - Guided to improvise my project board.

## Media
Banner image created for this project using Gemini.

# Acknowledgements: 
Special thanks to my tutors Emma Lamont, Idir and code institute.