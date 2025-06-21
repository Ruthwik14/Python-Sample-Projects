# Patient Appointment No-Show Analysis 🗓️

## Project Overview

This project analyzes a dataset of medical appointments in Brazil to identify the key factors contributing to patient no-shows. With approximately 30% of scheduled appointments being missed, understanding these underlying factors is critical for healthcare providers. The goal is to predict and pinpoint the most influential elements affecting patient attendance, enabling clinics to implement targeted strategies to reduce no-show rates, optimize resource allocation, and improve healthcare access for all patients.

## Data Description 📊

The analysis utilizes a comprehensive dataset derived from 100,000 medical appointments in Brazil.

* **Type:** Tabular data, consisting of various numerical, categorical, and datetime features.
* **Size:** Over 110,000 records, with 14 original features.
* **Source:** This dataset was compiled for the purpose of understanding patient appointment attendance patterns.

Key features include:

* **Patient Information:** `PatientId`, `AppointmentID`, `Gender`, `Age`.
* **Scheduling Details:** `ScheduledDay` (when the appointment was scheduled), `AppointmentDay` (the actual appointment date).
* **Location:** `Neighbourhood` (location of the hospital).
* **Medical Conditions & Assistance:** `Scholarship` (whether the patient is enrolled in a welfare program), `Hipertension`, `Diabetes`, `Alcoholism`, `Handcap` (number of disabilities).
* **Communication:** `SMS_received` (whether an SMS reminder was sent).
* **Target Variable:** `No-show` (indicating if the patient missed their appointment: 'Yes' or 'No').

## Methodology / Approach 🔬

This project followed a structured Exploratory Data Analysis (EDA) approach:

1.  **Data Loading and Initial Assessment:**
    * Loaded the dataset using `pandas` and performed initial inspections to understand its structure, identify data types, and check for basic information.
        ```python
        import pandas as pd
        import numpy as np
        import seaborn as sns
        import matplotlib.pyplot as plt

        data = pd.read_csv('Dataset.csv')
        print(data.head())
        print(data.info())
        ```

2.  **Data Cleaning and Preprocessing:**
    * **Irrelevant Columns:** Dropped `PatientId` and `AppointmentID` as they were not directly useful for analyzing no-show factors.
        ```python
        data = data.drop(['PatientId', 'AppointmentID'], axis=1)
        ```
    * **Date Type Conversion:** Converted `ScheduledDay` and `AppointmentDay` to datetime objects for accurate temporal analysis.
        ```python
        data['ScheduledDay'] = pd.to_datetime(data['ScheduledDay'], errors='coerce')
        data['AppointmentDay'] = pd.to_datetime(data['AppointmentDay'], errors='coerce')
        ```
    * **Invalid Age Values:** Removed records where `Age` was found to be -1, as this represents invalid data.
        ```python
        data = data[data['Age'] > 0]
        ```
    * **Handicap Simplification:** Filtered `Handcap` values to be less than 2, assuming higher values might indicate data anomalies or categories not relevant to the main analysis of attendance.
        ```python
        data = data[data['Handcap'] < 2]
        ```
    * **Missing Values & Duplicates:** Confirmed no missing values or duplicate records after initial loading, ensuring a clean dataset.
        ```python
        print(data.isnull().sum())
        print(data.duplicated().sum())
        ```

3.  **Exploratory Data Analysis (EDA):**
    * **Summary Statistics:** Generated descriptive statistics to understand the distribution and characteristics of numerical variables.
        ```python
        print(data.describe())
        ```
    * **Univariate Analysis:** Explored the distribution of individual features.
    * **Bivariate Analysis:** Investigated relationships between variables and the `No-show` target variable. This included analyzing:
        * Gender vs. Attendance
        * Neighborhood vs. Attendance
        * Age vs. Attendance
        * Disease type (Hypertension, Diabetes, Alcoholism, Handcap) vs. Attendance
        * SMS Received vs. Attendance
    * **Visualizations:** Used `matplotlib` and `seaborn` to create plots (e.g., bar plots, histograms) to visualize these relationships and patterns.
        ```python
        # Example: No-show distribution by Gender
        plt.figure(figsize=(6, 4))
        sns.countplot(data=data, x='Gender', hue='No-show')
        plt.title('Appointment No-show by Gender')
        plt.show()
        ```

## Key Results and Insights 💡

* **Overall No-Show Rate:** Approximately 30% of patients missed their scheduled appointments, highlighting a significant challenge.
* **Gender and Age Influence:** Females and younger patients tend to show up for their appointments more frequently than males and older patients. This challenges the common assumption that older individuals prioritize health appointments more.
* **Neighborhood Impact:** The specific neighborhood of the hospital appears to influence patient attendance, suggesting that factors like accessibility or local health infrastructure may play a role.
* **Disease Correlation:** Patients with hypertension show a tendency to attend appointments regardless of infection status, indicating that certain chronic conditions might act as a stronger motivator for attendance.
* **SMS Reminders:** The analysis explored the effectiveness of SMS reminders, providing insights into their potential impact on show-up rates.

## Tools and Technologies Used 🛠️

* **Programming Language:** Python
* **Libraries:**
    * `pandas`: For data manipulation and analysis.
    * `numpy`: For numerical operations.
    * `matplotlib.pyplot`: For creating static and dynamic visualizations.
    * `seaborn`: For high-level statistical data visualization.

## How to Use / Run the Project 🚀

1.  **Clone the Repository:**
    `git clone <repository_url>`
2.  **Navigate to the Project Directory:**
    `cd <project_directory>`
3.  **Install Dependencies:** Ensure you have Python installed. Then, install the required libraries:
    `pip install pandas numpy matplotlib seaborn`
4.  **Run the Jupyter Notebook:** Open the `Patient Appointment No Show Factors, EDA, Analysis.ipynb` notebook in a Jupyter environment (e.g., Jupyter Notebook, JupyterLab, VS Code with Jupyter extension).
    `jupyter notebook "Patient Appointment No Show Factors, EDA, Analysis.ipynb"`
5.  **Execute Cells:** Run the cells sequentially to reproduce the data cleaning, EDA, and generate the insights.

## Business Impact / Why this project is valuable ✨

This project offers valuable insights for healthcare administrators and policymakers to improve patient attendance and optimize clinic operations:

* **Targeted Interventions:** Develop more effective strategies to reduce no-shows by focusing on specific demographics (e.g., older male patients) or neighborhoods with lower attendance rates.
* **Resource Optimization:** Better predict patient attendance, allowing for more efficient scheduling of staff and resources, reducing wasted time and improving clinic flow.
* **Improved Patient Care:** Ensure more patients receive the care they need by addressing barriers to attendance.
* **Enhanced Communication:** Tailor reminder systems (e.g., SMS, calls) based on patient characteristics to maximize their effectiveness.
* **Cost Reduction:** Minimize the financial impact of missed appointments, which often include administrative overheads and underutilized clinical capacity.

Ultimately, this analysis contributes to creating a more efficient and patient-centric healthcare system.

## Contact Information / About Me 📧

**Devanapalli Ruthwik**
**Senior Data Analyst | Business Consultant**

**Email**: ruthwik.devanapalli@gmail.com
**LinkedIn**: <https://www.linkedin.com/in/ruthwik-devanapalli/>

This project is intended for educational, portfolio, and demonstration purposes. Attribution appreciated when used or adapted.