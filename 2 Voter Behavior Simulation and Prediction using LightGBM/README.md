
# 🇺🇸 U.S. Survey Data Simulator for Scalable Bayesian Modeling

## 🧠 Project Overview

Survey data is a powerful tool for understanding public sentiment, policy support, and demographic trends. However, real-world datasets often suffer from limitations such as missing values, demographic imbalances, and restricted sample sizes. These issues can hinder robust model development and generalization—especially in techniques that require large, diverse, and well-structured data.

In this project, I developed a custom **data simulator and generator for U.S. survey data** to complement downstream Bayesian modeling efforts. The simulator creates **synthetic but realistic survey datasets** that reflect known demographic distributions and observed response patterns from actual U.S. public opinion data.

The ultimate goal of this tool is to provide a **sandbox environment** for stress-testing predictive models, exploring "what-if" scenarios, and supporting data-driven policy simulations—while overcoming the limitations of real survey data.

---

## 📊 Data Description

The simulator was built using a cleaned and structured base dataset of real U.S. survey responses.

### ✅ Real Survey Data
- **File Used**: `usa survey data main after cleaning.xlsx`
- **Total Records**: ~20,000
- **Coverage**: All 50 U.S. states
- **Variables Included**:
  - Demographics: Gender, Age Group, Race, Education, Income, Political Affiliation, State
  - Outcomes: Binary opinion responses (e.g., support/oppose policies, views on key issues)

### 🔄 Synthetic Data Output
- Generated based on weighted sampling of distributions from the real dataset
- Statistically mirrors population characteristics and trends
- Can be scaled to simulate 100K+ records across multiple demographic combinations

---

## 🔍 Methodology / Project Workflow

The process was divided into the following phases:

### 1. **Data Cleaning and Standardization**
- Removed nulls and inconsistencies
- Re-coded categorical values for readability and grouping
- Standardized demographic buckets (e.g., income ranges, education levels)

### 2. **Exploratory Analysis**
- Analyzed feature distributions and correlations between variables
- Identified gaps in demographic representation
- Measured base rates of responses across groups (e.g., support rate by state or gender)

### 3. **Simulation Engine Design**
- Built a generator function to simulate new survey rows:
  - Uses **weighted probabilities** derived from real data
  - Ensures **realistic combinations** of demographic and geographic attributes
- Encoded dependencies between features using conditional probability where needed
- Scalable architecture allows rapid generation of large datasets

### 4. **Validation**
- Visual validation using histograms and bar charts
- Summary statistics comparison between real and simulated datasets
- Spot-checked joint distributions (e.g., opinion by education & state)

---

## 📈 Key Results and Highlights

- Successfully created a simulation pipeline that generates synthetic survey data **closely resembling real U.S. trends**.
- Simulated data exhibits **realistic distributions** across:
  - States and regions
  - Gender, income, education, and political affiliation
  - Opinion responses with noise and variability
- The output data can be used to:
  - Train and test Bayesian or ML models
  - Experiment with policy scenarios (e.g., "What if X% of young voters changed their views?")
  - Safely share synthetic data without compromising privacy

---

## ⚙️ Tools and Technologies Used

- **Python** – core scripting and simulation
- **Pandas, NumPy** – data wrangling, transformations, and probabilistic sampling
- **Seaborn, Matplotlib** – validation through visual exploration
- **Jupyter Notebook** – development and documentation

---

## ▶️ How to Use / Run the Project

To replicate the simulation:

1. **Clone the repository**  
   ```bash
   git clone https://github.com/your-username/usa-survey-simulator.git
   cd usa-survey-simulator
   ```

2. **Install dependencies**  
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the notebook**  
   ```bash
   jupyter notebook "USA simulater and data generater.ipynb"
   ```

4. **Follow the notebook steps**  
   - Load and explore real survey data
   - Generate synthetic data
   - Visualize and export for modeling use

> You can configure the simulator to adjust sample size, targeted demographics, or output features.

---

## 💼 Business Impact / Why This Project Is Valuable

This simulator adds **practical value to data science workflows** in scenarios where:

- **Real data is unavailable, incomplete, or imbalanced**
- **Stress-testing predictive models** across demographic segments is necessary
- **Synthetic data is required for privacy or ethical concerns**
- **Scenario modeling** is needed to inform strategic decisions or policy making

It empowers data teams, researchers, and policymakers to:
- **Prototype models without risking privacy**
- **Run "what-if" simulations** across regions and populations
- **Enhance Bayesian model training** with complete, scalable datasets

---

## 👤 About Me

**Ruthwik**  
Senior Data Analyst | Data Scientist | Automation & Simulation Specialist  

- 🔬 Expert in Bayesian modeling, survey analytics, and synthetic data generation  
- 🔧 Skilled in designing tools to automate and scale data science workflows  
- 🌍 Passionate about using data for social impact, equity, and evidence-based decisions  

📫 **Contact**  
Email: your.email@example.com  
LinkedIn: [LinkedIn Profile](#)

---

