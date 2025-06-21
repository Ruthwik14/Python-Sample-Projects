# Employee Attrition Case Study 📊

## Project Overview

This project delves into analyzing employee data to understand and identify the key factors contributing to employee attrition within a company. Employee attrition can lead to significant costs and operational challenges for any organization. By investigating patterns and trends in employee data, this study aims to uncover actionable insights that can help improve employee retention, reduce turnover rates, and foster a more stable and productive workforce.

## Data Description 📋

The analysis utilizes a comprehensive dataset containing various attributes related to employees.

* **Type:** Tabular data, comprising both numerical and categorical features.
* **Size:** The dataset contains approximately 4,410 records and 21 features.
* **Source:** This dataset was provided for the purpose of an analytical case study on employee attrition.

Key features include:
* **Demographic Information:** Age, Gender, Marital Status, Education, Education Field.
* **Employment Details:** Department, Job Role, Job Level, Business Travel, Distance From Home.
* **Compensation & Performance:** Monthly Income, Percent Salary Hike, Stock Option Level.
* **Work Experience:** Num Companies Worked, Total Working Years, Years At Company, Years Since Last Promotion, Years With Current Manager, Training Times Last Year.
* **Target Variable:** `Attrition` (indicating whether an employee left the company: 'Yes' or 'No').

## Methodology / Approach 🔬

This project followed a robust analytical approach:

1.  **Data Health Review and Preprocessing:**
    * **Loading and Initial Inspection:** The dataset was loaded using Python's `pandas` library, and an initial assessment of data types and non-null counts was performed.
        ```python
        import pandas as pd
        df = pd.read_excel('Employee Attrition DataSet.xlsx', 'Data')
        print(df.head())
        print(df.info())
        ```
    * **Missing Value Handling:** Identified columns with missing values (`NumCompaniesWorked` and `TotalWorkingYears`). Given the very small percentage of missing data (0.63% of total records), these rows were dropped to maintain data quality without significant loss.
        ```python
        total_null_val = df.isnull().sum()
        percent_null_val = (total_null_val / df.shape[0]) * 100
        print(percent_null_val)
        df.dropna(inplace=True)
        print(df.shape) # Check shape after dropping nulls
        ```
    * **Data Type Correction:** Converted relevant columns (`EmployeeID`, `Education`, `JobLevel`, `NumCompaniesWorked`, `TotalWorkingYears`) to appropriate data types (e.g., `object` for categorical IDs, `int` for whole numbers).
        ```python
        df['EmployeeID'] = df['EmployeeID'].astype(object)
        df['Education'] = df['Education'].astype(object)
        df['JobLevel'] = df['JobLevel'].astype(object)
        df['NumCompaniesWorked'] = df['NumCompaniesWorked'].astype(int)
        df['TotalWorkingYears'] = df['TotalWorkingYears'].astype(int)
        print(df.info()) # Verify changes
        ```
    * **Duplicate Check:** Verified that no duplicate records existed in the dataset.
        ```python
        print(df.duplicated().sum())
        ```
    * **Outlier Detection:** Explored outliers in numerical features using descriptive statistics and visualizations.

2.  **Exploratory Data Analysis (EDA):**
    * **Univariate Analysis:** Examined the distributions of individual variables (both numerical and categorical) to understand their characteristics.
        ```python
        # Example: Unique values for all columns
        for column in df.columns:
            print(f"Unique values in {column}: {df[column].unique()}")
        ```
    * **Bivariate Analysis:** Investigated relationships between variables, particularly focusing on how different factors relate to employee attrition using cross-tabulations and comparative visualizations.
    * **Attrition Rate Calculation:** Determined the overall attrition rate and analyzed attrition across different segments (e.g., age groups, departments).

3.  **KPI/Metric-based Questions:**
    * Analyzed specific business questions related to attrition drivers, such as the impact of salary increments, promotions, and manager relationships.

## Key Results and Insights 💡

* **Attrition Demographics:** Employee attrition is notably higher among younger employees (25-35 years old), especially those with fewer years at the company and less overall working experience.
* **Managerial Impact:** A significant number of departing employees had less than two years working with their last manager, suggesting a potential correlation between manager-employee relationships and attrition.
* **Compensation and Development:** Lower salary increments were observed to correlate with higher attrition rates. Additionally, insufficient training time spent in the last year appears to be a factor.
* **Identified Attrition Drivers:** Strong drivers of attrition include low salary increments, lack of promotion, manager-related issues, and a desire for change after a long tenure.
* **Imbalanced Dataset:** The dataset is imbalanced, with a majority of records representing employees who did not attrite. This was noted for potential future modeling considerations.

## Tools and Technologies Used 🛠️

* **Programming Language:** Python
* **Libraries:**
    * `pandas`: For data manipulation and analysis.
    * `numpy`: For numerical operations.
    * `matplotlib.pyplot`: For creating static, interactive, and animated visualizations.
    * `seaborn`: For high-level statistical data visualization.
    * `scipy.stats`: For statistical functions (e.g., probability distributions, hypothesis testing).
    * `statsmodels.api`: For statistical modeling.
    * `plotly.express`: For interactive visualizations.

## How to Use / Run the Project 🚀

1.  **Clone the Repository:**
    `git clone <repository_url>`
2.  **Navigate to the Project Directory:**
    `cd <project_directory>`
3.  **Install Dependencies:** Ensure you have Python installed. Then, install the required libraries:
    `pip install pandas numpy matplotlib seaborn scipy statsmodels plotly`
4.  **Run the Jupyter Notebook:** Open the `Employee Attrition Case Study Solution.ipynb` notebook in a Jupyter environment (e.g., Jupyter Notebook, JupyterLab, VS Code with Jupyter extension).
    `jupyter notebook "Employee Attrition Case Study Solution.ipynb"`
5.  **Execute Cells:** Run all cells sequentially to replicate the data cleaning, EDA, and generate the insights.

## Business Impact / Why this project is valuable ✨

This project provides critical insights for human resources and management teams to strategically address employee attrition. By understanding the key factors, the company can:

* **Optimize Retention Strategies:** Develop targeted interventions such as revised compensation policies, enhanced training programs, and manager development initiatives.
* **Improve Hiring Practices:** Re-evaluate hiring strategies to ensure better long-term fit, especially for newly hired employees who might be prone to early attrition.
* **Enhance Employee Satisfaction:** Create a more supportive and engaging work environment by addressing concerns related to management and career growth.
* **Reduce Operational Costs:** Lower recruitment and training costs associated with high turnover, leading to significant savings.
* **Foster Sustainable Growth:** Build a stable and experienced workforce that contributes consistently to organizational goals.

The findings empower the company to make data-driven decisions that enhance employee well-being and drive long-term business success.

## Contact Information / About Me 📧

**Devanapalli Ruthwik**
**Senior Data Analyst | Business Consultant**

**Email**: ruthwik.devanapalli@gmail.com
**LinkedIn**: <https://www.linkedin.com/in/ruthwik-devanapalli/>

This project is intended for educational, portfolio, and demonstration purposes. Attribution appreciated when used or adapted.