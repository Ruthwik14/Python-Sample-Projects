# Credit Card Default Prediction for HV Turnkey Lender 💳

## Project Overview

This project focuses on analyzing credit card customer data to identify key factors that contribute to payment defaults. For a financial institution like Turnkey Lender, understanding these factors is crucial for minimizing financial losses, effectively managing risk, and ultimately enhancing customer satisfaction. By leveraging data analysis and statistical techniques, this project aims to provide actionable insights that can inform strategic business decisions, improve marketing effectiveness, and optimize customer targeting.

## Data Description 📊

The analysis utilizes a comprehensive dataset providing information on credit card clients from April to September 2005.

* **Type:** Tabular data, primarily numerical and categorical.

* **Size:** Approximately 30,000 records, with 25 distinct features.

* **Source:** Provided by Turnkey Lender for the purpose of this analysis.

Key variables include:

* **Demographic Factors:** Gender, Education, Marital Status, Age.

* **Credit Data:** Amount of given credit.

* **Payment History:** Repayment status for the past six months (e.g., `REPAY_SEP`, `REPAY_AUG`).

* **Bill Statements:** Amount of bill statements for the past six months (e.g., `AMTBILL_SEP`, `AMTBILL_AUG`).

* **Previous Payments:** Amount of previous payments for the past six months.

* **Target Variable:** `DEF_AMT` (indicating whether a customer defaulted: 1 = Yes, 0 = No).

## Methodology / Approach 🔬

This project followed a structured data analysis approach:

1.  **Data Cleaning and Preprocessing:**

    * **Loading and Inspection:** Loaded the raw data using Python's `pandas` library and performed initial checks on data types and basic statistics.

        ```python
        import pandas as pd
        df = pd.read_csv('Dataset.csv')
        print(df.head())
        print(df.info())

        ```

    * **Missing Values:** Identified and handled missing values (specifically in the 'EDUCATION' column, which had a very small percentage of nulls, leading to their removal).

        ```python
        print(df.isnull().sum())
        # Example: df.dropna(subset=['EDUCATION'], inplace=True)

        ```

    * **Duplicate Records:** Checked for and confirmed the absence of duplicate records to ensure data uniqueness.

        ```python
        print(df.duplicated().sum())

        ```

    * **Data Consistency:** Explored and addressed negative values in bill statement columns, considering their interpretation as potential credits or data entry errors.

2.  **Exploratory Data Analysis (EDA):**

    * **Data Structure Examination:** Conducted a thorough examination of the dataset's structure, distributions, and unique values using Python functions.

    * **Statistical Summaries:** Calculated descriptive statistics (mean, median, standard deviation) to summarize key features and uncover initial trends.

        ```python
        print(df.describe())

        ```

    * **Visualizations:** Utilized Python libraries like `matplotlib` and `seaborn` to create visualizations (e.g., pie charts for defaulter percentages, histograms for repayment statuses) to uncover initial patterns and relationships between variables.

        ```python
        import matplotlib.pyplot as plt
        import seaborn as sns

        # Example: Distribution of age
        plt.figure(figsize=(8, 6))
        sns.histplot(df['AGE'], kde=True)
        plt.title('Distribution of Age')
        plt.xlabel('Age (Years)')
        plt.ylabel('Count')
        plt.show()

        ```

3.  **Inferential Statistics and Hypothesis Testing:** (Planned next steps based on the problem statement, to be implemented for deeper insights).

    * This phase will involve using statistical distributions, confidence intervals, and various hypothesis tests (t-test, F-test, ANOVA, Chi-Square) to rigorously identify significant factors influencing credit card defaults.

## Key Results (Current & Anticipated) 💡

* **Default Rate:** The initial analysis revealed that approximately 22.13% of credit card clients in the dataset defaulted on their payments. This highlights a significant area for intervention.

* **Data Quality:** Successfully cleaned the dataset by addressing missing values and confirming no duplicates, ensuring data reliability for further analysis.

* **Initial Insights from EDA:** Identified potential areas for deeper investigation, such as the distribution of repayment statuses and the presence of negative values in bill statements which may require specific handling or interpretation (e.g., as credits).

* **Anticipated Insights:** Through inferential statistics, we expect to pinpoint specific demographic, credit, or behavioral patterns that strongly correlate with default risk, enabling targeted strategies.

## Tools and Technologies Used 🛠️

* **Programming Language:** Python

* **Libraries:**

    * `pandas`: For data manipulation and analysis.

    * `numpy`: For numerical operations.

    * `matplotlib.pyplot`: For data visualization.

    * `seaborn`: For enhanced statistical data visualization.

## How to Use / Run the Project 🚀

1.  **Clone the Repository:**
    `git clone <repository_url>`

2.  **Navigate to the Project Directory:**
    `cd <project_directory>`

3.  **Install Dependencies:** Ensure you have Python installed. Then, install the required libraries:
    `pip install pandas numpy matplotlib seaborn`

4.  **Run the Jupyter Notebook:** Open the `Credit card default for HV Turnkey Lender.ipynb` notebook in a Jupyter environment (e.g., Jupyter Notebook, JupyterLab, VS Code with Jupyter extension).
    `jupyter notebook "Credit card default for HV Turnkey Lender.ipynb"`

5.  **Execute Cells:** Run the cells sequentially to reproduce the data cleaning, EDA, and initial findings.

## Business Impact / Why this project is valuable ✨

This project provides a robust analytical foundation for a credit card company to make data-driven decisions. By identifying the root causes of credit card defaults, Turnkey Lender can:

* **Reduce Financial Losses:** Implement proactive risk mitigation strategies.

* **Improve Risk Assessment:** Develop more accurate models for credit approval and setting credit limits.

* **Enhance Customer Satisfaction:** Tailor product offerings and communication strategies to better serve different customer segments, potentially reducing defaults through financial education and incentives.

* **Optimize Marketing Efforts:** Design targeted campaigns that resonate with specific customer profiles identified as lower risk or more likely to respond positively to interventions.

Ultimately, this analysis empowers the company to foster sustainable business growth by making smarter, more informed operational and strategic choices.

## Contact Information / About Me 📧

**Devanapalli Ruthwik**
**Senior Data Analyst | Business Consultant**

**Email**: ruthwik.devanapalli@gmail.com
**LinkedIn**: <https://www.linkedin.com/in/ruthwik-devanapalli/>

This project is intended for educational, portfolio, and demonstration purposes. Attribution appreciated when used or adapted.