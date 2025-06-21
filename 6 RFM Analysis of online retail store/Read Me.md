# RFM Analysis of Online Retail Data 🛍️

## Project Overview

This project focuses on applying **RFM (Recency, Frequency, Monetary) analysis** to an online retail dataset. RFM analysis is a powerful customer segmentation technique commonly used in marketing and sales. The goal is to understand customer behavior by identifying how recently they made a purchase (Recency), how often they purchase (Frequency), and how much they spend (Monetary Value). This analysis provides valuable insights for businesses to tailor marketing strategies, improve customer retention, and optimize revenue generation.

## Data Description 📊

The analysis uses a comprehensive online retail transaction dataset.

* **Type:** Tabular data, containing transactional information.
* **Size:** Over 1 million entries, with 8 key features.
* **Source:** An online retail dataset.

Key features include:

* **Invoice:** Invoice number.
* **StockCode:** Product (item) code.
* **Description:** Product description.
* **Quantity:** The quantity of each item purchased.
* **InvoiceDate:** Date and time of the invoice.
* **Price:** Unit price of the product.
* **Customer ID:** Unique identifier for each customer.
* **Country:** Country where the customer resides.

## Methodology / Approach 🔬

This project followed a structured data preparation and RFM analysis approach:

1.  **Data Preparation and Cleaning:**
    * **Loading and Initial Inspection:** Loaded the raw data using `pandas` and performed initial checks on data types and structure.
        ```python
        import pandas as pd
        import numpy as np
        import datetime

        df = pd.read_csv("Dataset.csv")
        print(df.head())
        print(df.info())
        ```
    * **Data Type Conversion:**
        * The 'Price' column, initially an object due to comma decimals, was cleaned by replacing commas with dots and converted to `float`.
            ```python
            df['Price'] = df['Price'].str.replace(',', '.').astype(float)
            ```
        * The 'InvoiceDate' column was converted to a datetime object to enable temporal calculations.
            ```python
            df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], errors='coerce')
            ```
        * The 'Customer ID' column was cleaned (removing '.0') and converted to `object` type for consistency.
            ```python
            df['Customer ID'] = df['Customer ID'].astype(str).apply(lambda x: x.replace('.0', ''))
            df.rename(columns={'Customer ID': 'Customer_ID'}, inplace=True)
            ```
    * **Feature Engineering:** A new column, `Tot_Rev` (Total Revenue), was created by multiplying `Price` and `Quantity`.
        ```python
        df["Tot_Rev"] = (df['Price'] * df['Quantity'])
        ```
    * **Missing Values & Irrelevant Records:** Missing values, particularly in 'Customer_ID' (represented as 'nan' strings after conversion), were identified and removed, ensuring that only valid customer data was used for analysis.
        ```python
        df = df.dropna() # Handles NaN from initial load or after transformations
        df.drop(df[df['Customer_ID'] == 'nan'].index, inplace=True)
        ```
    * **Sorting Data:** The DataFrame was sorted by `Customer_ID` to facilitate grouped calculations.

2.  **RFM Analysis Implementation:**
    * **Recency Calculation:**
        * A reference 'today's date' (`1.1.2012`) was set.
        * The `MAX_InvoiceDate` (most recent purchase date) was calculated for each customer.
        * Recency (`duration`) was then calculated as the difference between 'today's date' and `MAX_InvoiceDate`.
        ```python
        RFM = pd.DataFrame() # Initialize RFM DataFrame
        RFM['order_date'] = pd.to_datetime('1.1.2012 00:00')
        RFM['MAX_InvoiceDate'] = df.groupby("Customer_ID")['InvoiceDate'].max()
        RFM['duration'] = RFM['order_date'] - RFM['MAX_InvoiceDate']
        ```
    * **Frequency Calculation:** Counted the number of unique invoices (or items) per customer.
        ```python
        RFM['Freq'] = df.groupby("Customer_ID").StockCode.count()
        ```
    * **Monetary Value Calculation:** Summed the total revenue for each customer.
        ```python
        RFM['Tot_Rev'] = df.groupby("Customer_ID").Tot_Rev.sum()
        RFM['Avg_Rev'] = RFM['Tot_Rev'] / RFM['Freq'] # Also calculated Average Revenue
        ```
    * **Customer Segmentation:** Created 10 different decile buckets for Recency (`Recency_Deciles`) to segment customers based on how recently they purchased.
        ```python
        RFM['Recency_Deciles'] = pd.qcut(RFM['duration'], 10)
        ```
    * **Cumulative Revenue Analysis:** Analyzed cumulative revenue across these Recency deciles to understand the contribution of different customer segments.

## Key Results and Insights 💡

* **Customer Value Segmentation:** The RFM analysis successfully segmented customers based on their purchase behavior:
    * **Recency:** Identified groups of customers who have purchased very recently versus those who have not purchased for a long time. This is crucial for re-engagement campaigns.
    * **Frequency:** Quantified how often customers make purchases, allowing identification of loyal, repeat buyers.
    * **Monetary Value:** Determined which customers contribute the most revenue, highlighting high-value customer segments.
* **Revenue Concentration:** Analysis of cumulative revenue by Recency deciles showed that a significant portion of total revenue comes from customers who have purchased more recently. This reinforces the importance of targeting recent customers.
* **Data Preparedness:** The project successfully cleaned and transformed a large, raw transactional dataset into a structured format suitable for advanced customer analytics.

## Tools and Technologies Used 🛠️

* **Programming Language:** Python
* **Libraries:**
    * `pandas`: For robust data manipulation, cleaning, and aggregation.
    * `numpy`: For numerical operations.
    * `datetime`: For handling and calculating with dates and times.

## How to Use / Run the Project 🚀

1.  **Clone the Repository:**
    `git clone <repository_url>`
2.  **Navigate to the Project Directory:**
    `cd <project_directory>`
3.  **Install Dependencies:** Ensure you have Python installed. Then, install the required libraries:
    `pip install pandas numpy`
4.  **Run the Jupyter Notebook:** Open the `RFM Analysis of online retail Store.ipynb` notebook in a Jupyter environment (e.g., Jupyter Notebook, JupyterLab, VS Code with Jupyter extension).
    `jupyter notebook "RFM Analysis of online retail Store.ipynb"`
5.  **Execute Cells:** Run all cells sequentially to perform the data preparation, RFM calculations, and view the results.

## Business Impact / Why this project is valuable ✨

RFM analysis is a cornerstone of effective customer relationship management (CRM) and marketing strategy. This project demonstrates the ability to:

* **Enhance Marketing ROI:** Enable businesses to design personalized marketing campaigns for different customer segments, leading to higher conversion rates and better allocation of marketing spend. For example, recent, high-value customers can receive loyalty offers, while less recent customers can be targeted with re-engagement promotions.
* **Improve Customer Retention:** Identify at-risk customers (those with high recency) and develop proactive retention strategies.
* **Optimize Product Offerings:** Understand which customer segments are most valuable and what they typically purchase, informing product development and inventory management.
* **Maximize Lifetime Value:** By focusing on the most valuable customer segments, businesses can increase the average customer lifetime value.
* **Data-Driven Decision Making:** Provide a clear, quantifiable framework for understanding customer behavior, moving beyond anecdotal evidence to strategic, data-informed decisions.

## Contact Information / About Me 📧

**Devanapalli Ruthwik**
**Senior Data Analyst | Business Consultant**

**Email**: ruthwik.devanapalli@gmail.com
**LinkedIn**: <https://www.linkedin.com/in/ruthwik-devanapalli/>

This project is intended for educational, portfolio, and demonstration purposes. Attribution appreciated when used or adapted.