# 🇺🇸 U.S. Statewise Public Opinion Modeling Using Bayesian Hierarchical Logistic Regression

## Project Overview 📌

Public opinion significantly influences policy, social movements, and business strategies. However, relying solely on national sentiment can overlook crucial regional, demographic, and political variations. This project addresses this by developing a robust **Bayesian hierarchical logistic regression model** to analyze and predict public opinion across U.S. states. Using a large-scale survey dataset, the model identifies state-level differences in sentiment and pinpoints key factors driving opinions, such as education, gender, income, and political affiliation. The goal is to provide decision-makers in government, non-profits, and businesses with **data-driven insights** into how opinions differ across the country and what influences them.

## Data Description 📊

This project utilizes a curated and balanced public survey dataset reflecting social, political, and cultural attitudes of individuals across the U.S.

* **Type:** Tabular, public survey data.
* **Size:** Approximately 30,000 individual responses.
* **Geographic Coverage:** Includes data from all 50 U.S. states.
* **Key Data Files:**
    * `Balanced_US_Survey_With_All_Trends.xlsx`: Contains cleaned and balanced individual-level data with demographic information and various opinion variables.
    * `usa_statewise_survey.xlsx`: Aggregated survey responses by U.S. state.
    * `columns.xlsx`: Metadata providing explanations for column names and variable types.

**Included Demographics:** Age, Gender, Race, Education Level, Income, Political Affiliation.
**Outcome Variables:** Binary responses to opinion-based questions (e.g., support/opposition to an issue).

## Methodology / Approach 🔬

The analysis follows a structured data science workflow:

1.  **Data Preprocessing and Feature Engineering:**
    * **Data Loading:** Loaded the survey data using `pandas`.
        ```python
        import pandas as pd
        import numpy as np
        # ... other imports (pymc, arviz, matplotlib, seaborn)
        warnings.filterwarnings("ignore")

        # Assuming 'usa_survey_data_for_simulater.xlsx' or a similar file is loaded
        survey_df = pd.read_excel('usa_survey_data_for_simulater.xlsx', sheet_name='Sheet1')
        survey_df.columns = survey_df.columns.str.strip().str.lower()
        print(survey_df.head())
        ```
    * **Handling Missing Values:** Cleaned the dataset by dropping rows with missing values in critical target and demographic columns to ensure data quality.
        ```python
        raw_target_columns = [
            'Which party or candidate do you currently intend to vote for...',
            # ... rest of your target questions
        ]
        raw_demographic_columns = [
            'Age', 'Gender', 'Ethnicity', 'occupation',
            'total monthly household income before tax', 'education'
        ]
        target_columns = [col.strip().lower() for col in raw_target_columns]
        demographic_columns = [col.strip().lower() for col in raw_demographic_columns]

        survey_df = survey_df.dropna(subset=target_columns + demographic_columns + ['state'])
        print(f"Data shape after dropping missing values: {survey_df.shape}")
        ```
    * **Categorical Encoding:** Converted categorical demographic features into numerical codes suitable for modeling, and managed the categories.
        ```python
        # Example for one demographic column
        demo_codes = {}
        demo_cats = {}
        for col in demographic_columns:
            cat = pd.Categorical(survey_df[col].astype(str).str.strip())
            survey_df[f"{col}_code"] = cat.codes
            demo_codes[col] = survey_df[f"{col}_code"].values
            demo_cats[col] = cat
        print(survey_df[[f"{col}_code" for col in demographic_columns]].head())
        ```

2.  **Bayesian Modeling:**
    * Developed a **hierarchical logistic regression model** using the `PyMC` library. This model captures both individual-level variations and state-level group effects, allowing for more robust and nuanced insights compared to traditional regression.
    * Used **Markov Chain Monte Carlo (MCMC)** sampling to estimate the posterior distributions of model parameters, providing not just single estimates but also their associated uncertainty (credible intervals).
    * Diagnosed model convergence using standard statistical checks to ensure reliability of the results.
        ```python
        import pymc as pm
        import arviz as az

        # Assuming 'state_df' is a subset for a specific state and 'question' is a target column
        # and 'n_options' is the number of categories in the target variable
        # and 'target_cat' holds the categories for the specific question
        # and 'target_code' is the numerical encoding of the target

        # Simplified example for a single question and state for illustration
        with pm.Model() as model:
            # Hierarchical priors for demographic effects
            sigmas = {}
            a_demos = {}
            for col in demographic_columns:
                sigmas[col] = pm.HalfNormal(f"sigma_{col}", sigma=1)
                a_demos[col] = pm.Normal(f"a_{col}", mu=0, sigma=sigmas[col], shape=(len(demo_cats[col].categories), n_options))

            # Intercept for each option
            a = pm.Normal("a", mu=0, sigma=1, shape=n_options)

            # Combined effects (intercept + demographic effects)
            demo_effects = sum(a_demos[col][demo_codes[col]] for col in demographic_columns)
            logits = a + demo_effects

            # Likelihood for categorical response
            y_obs = pm.Categorical("y_obs", logit_p=logits, observed=state_df['target_code'])

            # MCMC sampling
            trace = pm.sample(500, tune=100, target_accept=0.95, random_seed=42, progressbar=False)

        print(az.summary(trace, var_names=["a"])) # Example: Summarize intercept posterior
        ```

3.  **Analysis & Visualization:**
    * Visualized the posterior distributions of key predictors to understand their impact.
    * Mapped predicted probabilities and opinion trends across U.S. states using tools like heatmaps and bar charts.
    * Calculated mean probabilities, standard deviations, and 'winning probabilities' for each opinion option.
        ```python
        # Softmax function to convert logits to probabilities
        def softmax(x):
            e_x = np.exp(x - np.max(x))
            return e_x / e_x.sum()

        logits_samples = trace.posterior["a"].stack(sample=("chain", "draw")).values.T
        probabilities = np.apply_along_axis(softmax, 1, logits_samples)

        mean_probs = probabilities.mean(axis=0)
        std_probs = probabilities.std(axis=0)
        winning_party_indices = np.argmax(probabilities, axis=1)
        winning_counts = np.bincount(winning_party_indices, minlength=n_options)
        winning_probabilities = winning_counts / probabilities.shape[0]

        print(f"Mean probabilities: {mean_probs}")
        print(f"Winning probabilities: {winning_probabilities}")
        ```

## Key Results and Insights 💡

* **Geographic Opinion Patterns:** The model successfully identified **clear geographic patterns** in public opinion, highlighting regional differences (e.g., higher support for progressive policies in Northeastern states vs. more conservative stances in Southern and Midwestern states).
* **Strong Predictors Identified:** **Education level, political affiliation, and income** consistently emerged as the strongest predictors influencing public opinion on various issues.
* **Uncertainty-Aware Predictions:** A key advantage of using Bayesian inference is the ability to represent uncertainty explicitly, providing **credible intervals** for all estimates. This makes the predictions more reliable and trustworthy for high-stakes decision-making.
* **Interpretable State-Level Insights:** The hierarchical structure of the model allowed for accurate modeling of state-level variations, making the derived insights highly **interpretable** and actionable for targeted interventions.

## Tools and Technologies Used 🛠️

* **Programming Language:** Python (Core programming language for all analysis)
* **Bayesian Modeling:** `PyMC` (for building and sampling from probabilistic models)
* **Statistical Analysis:** `ArviZ` (for Bayesian workflow, diagnostics, and visualization)
* **Data Manipulation:** `Pandas`, `NumPy` (for efficient data cleaning, transformation, and numerical operations)
* **Visualizations:** `Matplotlib`, `Seaborn` (for creating compelling and insightful data visualizations)
* **Environment:** `Jupyter Notebook` (for interactive development and analysis)

## How to Use / Run the Project 🚀

To replicate or run the analysis:

1.  **Clone the Repository:**
    ```bash
    git clone <repository_url>
    cd <project_directory>
    ```
2.  **Install Dependencies:** Ensure Python is installed. Then, install the required libraries (it's recommended to use a virtual environment):
    ```bash
    pip install -r requirements.txt # Assuming a requirements.txt is provided, or list them:
    # pip install pandas numpy pymc arviz matplotlib seaborn
    ```
3.  **Prepare Data:** Ensure `Balanced_US_Survey_With_All_Trends.xlsx` and `columns.xlsx` (or `usa_survey_data_for_simulater.xlsx` if it's the primary input) are in the project directory.
4.  **Open the Notebook:** Launch the Jupyter notebook file:
    ```bash
    jupyter notebook "usa data.ipynb" # Or "Bayesian hierarchical logistic regression model.ipynb"
    ```
5.  **Run Cells Sequentially:** Execute all cells in order within the notebook to load the data, preprocess it, fit the Bayesian model, and generate the visualizations and insights.

> ⚠️ **Note on Performance:** MCMC sampling can be computationally intensive. For optimal performance, consider running on a machine with multiple CPU cores.

## Business Impact / Why this project is valuable ✨

This project delivers **actionable, uncertainty-aware insights** into public opinion, which is invaluable for a wide range of stakeholders:

* **Government & Policy Makers:** Enables the design of more effective and targeted outreach programs and policies that resonate with specific regional populations.
* **Media & Advocacy Groups:** Provides a data-driven approach to target messages and campaigns to demographics and states most receptive to particular viewpoints.
* **Corporate Strategy & Marketing:** Helps businesses understand regional market perceptions, allowing for better brand alignment, product positioning, and localized marketing efforts.
* **Robust Decision-Making:** The use of Bayesian modeling provides not just predictions, but also the confidence intervals around those predictions, making the results more trustworthy for high-stakes decisions where understanding uncertainty is paramount.

This project showcases expertise in advanced statistical modeling and the ability to translate complex analytical findings into clear, actionable business recommendations.

## Contact Information / About Me 📧

**Devanapalli Ruthwik**
**Senior Data Analyst | Business Consultant**

**Email**: ruthwik.devanapalli@gmail.com
**LinkedIn**: <https://www.linkedin.com/in/ruthwik-devanapalli/>

This project is intended for educational, portfolio, and demonstration purposes. Attribution appreciated when used or adapted.