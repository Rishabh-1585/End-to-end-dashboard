# 📊 Sales Data Analysis & Power BI Dashboard

An end-to-end **Sales Data Analysis project** built using **Excel, Python (Pandas), MySQL, and Power BI**.

The project demonstrates a complete data analytics workflow — starting from raw sales data in Excel, cleaning and transforming the data using Python/Pandas, storing the cleaned dataset in MySQL, and finally creating an interactive Power BI dashboard for business analysis and visualization.

---

## 🚀 Project Overview

The main objective of this project is to analyze sales data and transform raw transactional data into a clean, structured, and visualization-ready dataset.

The project covers the complete analytics pipeline:

```text
Raw Excel Data
      ↓
Python + Pandas
      ↓
Data Cleaning & Transformation
      ↓
Cleaned CSV
      ↓
MySQL Database
      ↓
Power BI
      ↓
Interactive Sales Dashboard
```

---

## 🛠️ Tools & Technologies

| Tool                 | Purpose                          |
| -------------------- | -------------------------------- |
| **Microsoft Excel**  | Raw data source                  |
| **Python**           | Data processing and analysis     |
| **Pandas**           | Data cleaning and transformation |
| **Jupyter Notebook** | Python analysis environment      |
| **MySQL**            | Database storage                 |
| **SQLAlchemy**       | Python-MySQL connection          |
| **PyMySQL**          | MySQL database driver            |
| **Power BI**         | Data visualization and dashboard |

---

## 📁 Project Files

```text
Sales-Data-Analysis/
│
├── sale_data.xlsx
├── Sales_cleaned_data.csv
├── salesanalysis.ipynb
├── sales_dashboard.pbix
└── README.md
```

### File Description

**`sale_data.xlsx`**

Contains the original raw sales dataset.

Main columns:

* `Order_ID`
* `Order_Date`
* `Customer`
* `Region`
* `Product`
* `Sales`
* `Cost`

The raw dataset contains **520 records**.

---

**`salesanalysis.ipynb`**

Jupyter Notebook containing the Python/Pandas data cleaning and transformation process.

---

**`Sales_cleaned_data.csv`**

Cleaned and transformed dataset generated using Python/Pandas.

The final dataset contains **482 records** and includes additional analytical columns:

* `Profit`
* `Day`
* `Month`
* `Year`

---

**`sales_dashboard.pbix`**

Power BI dashboard file used for interactive sales analysis and visualization.

---

# 🔄 Data Analytics Workflow

## 1️⃣ Data Collection – Excel

The project starts with raw sales data stored in an Excel file.

The dataset contains information related to:

* Orders
* Order dates
* Customers
* Regions
* Products
* Sales
* Cost

Example:

| Order_ID | Order_Date | Customer | Region | Product | Sales |  Cost |
| -------: | ---------- | -------- | ------ | ------- | ----: | ----: |
|     1001 | 2023-01-13 | Rohit    | South  | Mobile  | 23289 | 19118 |
|     1002 | 2023-07-10 | Aman     | West   | Laptop  |  8905 |  5593 |

---

# 🐍 2️⃣ Data Cleaning Using Python & Pandas

Python and Pandas were used to clean and transform the raw Excel data.

### Import Pandas

```python
import pandas as pd
```

### Load Excel Data

```python
df = pd.read_excel("sale_data.xlsx")
```

The Excel dataset is loaded into a Pandas DataFrame for further processing.

---

## 🔍 Duplicate Value Check

Duplicate records were checked using:

```python
df.duplicated().sum()
```

Duplicate records were then removed:

```python
df = df.drop_duplicates()
```

This helps ensure that the analysis is not affected by duplicate transactions.

---

## 📅 Date Conversion

The `Order_Date` column was converted into a proper datetime format:

```python
df['Order_Date'] = pd.to_datetime(
    df['Order_Date'],
    errors='coerce'
)
```

Invalid date values are converted to `NaT`.

---

## 🧹 Remove Invalid Dates

Rows containing invalid/missing dates were removed:

```python
df = df.dropna(subset=['Order_Date'])
```

This ensures that date-based analysis can be performed correctly.

---

# 💰 3️⃣ Feature Engineering

Additional analytical columns were created using Pandas.

## Profit Calculation

Profit was calculated using:

```python
df['Profit'] = df['Sales'] - df['Cost']
```

### Formula

```text
Profit = Sales - Cost
```

---

## 📅 Extract Day, Month and Year

The following columns were created from `Order_Date`:

```python
df['Day'] = df['Order_Date'].dt.day
df['Month'] = df['Order_Date'].dt.month
df['Year'] = df['Order_Date'].dt.year
```

These columns make it easier to perform time-based analysis.

---

# 💾 4️⃣ Export Cleaned Data

After cleaning and transformation, the processed dataset was exported to CSV:

```python
df.to_csv(
    'Sales_cleaned_data.csv',
    index=False
)
```

The cleaned dataset contains:

```text
Order_ID
Order_Date
Customer
Region
Product
Sales
Cost
Profit
Day
Month
Year
```

---

# 🗄️ 5️⃣ MySQL Database

The cleaned CSV data was then loaded into MySQL.

SQLAlchemy was used to establish the connection between Python and MySQL.

```python
from sqlalchemy import create_engine
```

### Create Database Connection

```python
engine = create_engine(
    "mysql+pymysql://root:root@localhost:3306/salesdb"
)
```

The cleaned CSV was loaded into Pandas:

```python
df = pd.read_csv("Sales_cleaned_data.csv")
```

The data was then inserted into the MySQL table:

```python
df.to_sql(
    name="salesdata",
    con=engine,
    if_exists="replace",
    index=False
)
```

### MySQL Table

The cleaned sales data was stored in:

```text
salesdata
```

This step demonstrates how Python can be used to move processed data into a relational database for further analysis and reporting.

---

# 📊 6️⃣ Power BI Dashboard

The cleaned sales data was used in Power BI to create an interactive dashboard.

The Power BI file is:

```text
sales_dashboard.pbix
```

The dashboard provides a visual way to analyze sales performance across different dimensions such as:

* Sales
* Profit
* Region
* Product
* Customer
* Time

Power BI helps convert the processed data into interactive business insights.

---

# 📈 Key Analysis Areas

The project focuses on analyzing:

### 💰 Sales Performance

Understand overall sales performance across the dataset.

### 📦 Product Analysis

Compare sales performance between different products.

### 🌎 Regional Analysis

Analyze sales across different regions.

### 👤 Customer Analysis

Identify customer-level sales performance.

### 📅 Time-Based Analysis

Analyze sales and profit using:

* Day
* Month
* Year

### 💵 Profit Analysis

Compare sales and cost to understand profitability.

---

# 🧹 Data Cleaning Performed

The following data preparation steps were performed:

* Loaded raw Excel data using Pandas
* Checked duplicate records
* Removed duplicate records
* Converted order dates into datetime format
* Removed invalid date records
* Created Profit column
* Extracted Day from Order Date
* Extracted Month from Order Date
* Extracted Year from Order Date
* Exported cleaned data to CSV
* Loaded cleaned data into MySQL
* Prepared data for Power BI visualization

---

# 📊 Dataset Summary

| Dataset         | Records | Columns |
| --------------- | ------: | ------: |
| Raw Excel Data  |     520 |       7 |
| Cleaned Dataset |     482 |      11 |

### Raw Dataset Columns

```text
Order_ID
Order_Date
Customer
Region
Product
Sales
Cost
```

### Cleaned Dataset Columns

```text
Order_ID
Order_Date
Customer
Region
Product
Sales
Cost
Profit
Day
Month
Year
```

---

# 🎯 Project Objectives

The main objectives of this project are:

1. Understand the complete data analytics workflow.
2. Clean raw sales data using Python and Pandas.
3. Perform basic data transformation and feature engineering.
4. Calculate profit from sales and cost.
5. Store cleaned data in MySQL.
6. Connect different technologies in a single analytics workflow.
7. Build an interactive Power BI dashboard.
8. Generate meaningful business insights from sales data.

---

# 💡 Skills Demonstrated

This project demonstrates practical knowledge of:

* Excel
* Python
* Pandas
* Data Cleaning
* Data Transformation
* Feature Engineering
* DateTime Handling
* CSV Data Processing
* MySQL
* SQLAlchemy
* PyMySQL
* Database Connectivity
* Power BI
* Data Visualization
* Business Analysis
* End-to-End Data Analytics

---

# 🔗 End-to-End Architecture

```text
                    ┌─────────────────┐
                    │      Excel      │
                    │   Raw Dataset   │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │     Python      │
                    │     Pandas      │
                    │ Data Cleaning   │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │   Cleaned CSV   │
                    │ Transformed Data│
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │      MySQL      │
                    │   salesdata     │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │    Power BI     │
                    │    Dashboard    │
                    └─────────────────┘
```

---

# 📌 Conclusion

This project demonstrates an end-to-end **Data Analytics pipeline**, starting from raw Excel data and ending with an interactive Power BI dashboard.

By combining **Excel, Python/Pandas, MySQL, and Power BI**, the project shows how raw transactional data can be cleaned, transformed, stored, analyzed, and presented in a business-friendly format.

The project is suitable for demonstrating practical **Data Analyst skills** in a portfolio, GitHub repository, and interviews.

---

## 👨‍💻 Author

**Rishabh Sharma**

**B.Tech – Computer Science & Engineering**

Interested in **Data Analytics, Python, SQL, Excel, and Power BI**.

---

⭐ If you find this project useful, feel free to star the repository.
