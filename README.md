# 🛒 Superstore Sales Data — Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4C8CBF)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Project Overview

This project performs a comprehensive **Exploratory Data Analysis (EDA)** on the **Superstore Sales Dataset**, a retail transactions dataset containing order details, customer segments, product categories, and financial metrics.

The analysis is structured across two phases:

- **Phase 1 — Data Exploration & Initial Assessment:** Understanding the dataset's structure, identifying data quality issues, and profiling key columns.
- **Phase 2 — Data Cleaning, Manipulation & Visualization:** Resolving data quality issues, engineering clean data, and uncovering business insights through visualizations.

---

## 📂 Dataset Description

| Property | Details |
|---|---|
| **File** | `SuperstoreData.csv` |
| **Rows** | 9,994 |
| **Columns** | 21 |
| **Domain** | Retail / E-Commerce |

### Key Columns

| Column | Type | Description |
|---|---|---|
| `Order ID` | String | Unique order identifier |
| `Order Date` | Date | Date the order was placed |
| `Ship Date` | Date | Date the order was shipped |
| `Customer ID` | String | Unique customer identifier |
| `Segment` | Categorical | Customer segment (Consumer, Corporate, Home Office) |
| `Region` | Categorical | Geographic region (West, East, Central, South) |
| `Category` | Categorical | Product category (Furniture, Office Supplies, Technology) |
| `Sub-Category` | Categorical | Product sub-category |
| `Sales` | Float | Revenue from the order |
| `Quantity` | Integer | Units ordered |
| `Discount` | Float | Discount applied |
| `Profit` | Float | Net profit from the order |

---

## 🎯 Objectives

- Understand the structure, data types, and distribution of the Superstore dataset
- Identify and resolve data quality issues (missing values, duplicates, type errors, inconsistencies)
- Perform univariate, bivariate, and multivariate analysis
- Derive actionable business insights through statistical summaries and visualizations

---

## 🔧 Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, manipulation |
| `numpy` | Numerical operations and outlier detection |
| `matplotlib` | Custom visualizations and plots |
| `seaborn` | Statistical plots (boxplots, heatmaps, pairplots) |

---

## 📋 Project Structure

```
📁 Superstore-EDA/
│
├── 📓 EDA_Project.ipynb       # Main Jupyter Notebook (full analysis)
├── 📄 SuperstoreData.csv      # Raw dataset
└── 📄 README.md               # Project documentation
```

---

## 🔍 Phase 1 — Data Exploration & Initial Assessment

### Steps Performed

1. **Dataset Loading** — Loaded the CSV and confirmed shape: `9,994 rows × 21 columns`
2. **Structure Inspection** — Reviewed column names, data types, and non-null counts using `.info()`
3. **Summary Statistics** — Generated descriptive stats for numeric and categorical columns using `.describe()`
4. **Missing Value Analysis** — Identified null entries using `.isnull().sum()`; computed percentage of missing data per column
5. **Category Distribution** — Counted frequency of values in `Category`, `Region`, and `Segment` columns
6. **Outlier Detection** — Applied IQR method to flag extreme values in `Sales`, `Profit`, `Quantity`, and `Discount`
7. **Data Quality Assessment** — Reviewed type mismatches, text inconsistencies, and structural issues

### Key Findings

| Issue | Detail |
|---|---|
| Missing values | `Sales` (50 nulls), `Profit` (40 nulls), `Region` (30 nulls) |
| Type mismatch | `Order Date` and `Ship Date` stored as `object` instead of `datetime` |
| Outliers | High-value extremes present in `Sales` and `Profit` |
| Categorical consistency | Mixed casing and whitespace detected in text columns |

---

## 🧹 Phase 2 — Data Cleaning, Manipulation & Visualization

### Data Cleaning Steps

| Step | Action | Justification |
|---|---|---|
| Missing — Numeric | Filled `Sales` and `Profit` nulls with **median** | Median is robust to outliers |
| Missing — Categorical | Filled `Region` nulls with **mode** | Preserves real geographic distribution |
| Duplicates | Removed complete duplicate rows with `drop_duplicates(keep='first')` | Prevents overcounting in aggregates |
| Date Conversion | Converted `Order Date` and `Ship Date` to `datetime64[ns]` | Enables time-series and date calculations |
| Categorical Standardization | Applied `.str.lower()` and `.str.strip()` on all text columns | Ensures consistent grouping |
| Outlier Treatment | Winsorized extremes using IQR boundaries | Reduces influence without removing data points |
| Type Casting | Cast numeric columns to `float64`; category columns to `category` dtype | Improves performance and memory efficiency |

---

## 📊 Visualizations

### 1. Sales Distribution (Histogram)
- Sales are **right-skewed** — most orders fall under $500
- A small number of high-value orders ($5,000+) exist as outliers
- Justifies using **median** for missing value imputation

### 2. Profit by Category (Box Plot)
- **Technology** shows the highest median profit
- **Furniture** has the most negative profit outliers (losses)
- **Office Supplies** demonstrates the most consistent margins

### 3. Sales vs. Profit (Scatter Plot)
- Moderate positive correlation (`r = 0.48`)
- Several high-sales orders still generate **negative profit**, indicating cost/discount issues

### 4. Average Sales by Region (Bar Chart)
- **South** region generates the highest average sales per order
- **Central** region has the lowest average order value

### 5. Correlation Heatmap
| Pair | Correlation | Interpretation |
|---|---|---|
| Sales ↔ Quantity | r = +0.821 | Strong — higher volume drives higher revenue |
| Discount ↔ Profit | r = −0.394 | Negative — heavy discounting reduces margins |
| Sales ↔ Profit | r = +0.478 | Moderate — revenue alone doesn't guarantee profitability |

### 6. Sales by Region & Segment (Grouped Bar Chart)
- **Consumer** segment dominates in West and East regions
- **Corporate** segment shows consistent performance across all regions
- **Home Office** is the smallest segment — a potential growth opportunity

### 7. Orders by Category (Pie Chart)
- **Office Supplies** accounts for the highest share of orders
- **Technology** has fewer orders but higher profit margins

### 8. Pair Plot — Profit by Product Category
- **Technology** maintains higher profit margins across all sales levels
- **Furniture** shows higher profit volatility and more loss-making transactions

---

## 💡 Key Business Insights

1. **Discount Strategy Needs Review** — The negative correlation between Discount and Profit (`r = −0.394`) shows that excessive discounting significantly erodes margins.
2. **Technology is the Most Profitable Category** — Despite fewer orders, Technology products deliver higher profit per transaction.
3. **Furniture Has a Loss Problem** — Multiple Furniture orders generate negative profit; pricing or cost structures need reassessment.
4. **West & East Regions are High-Performers** — These regions should receive focused investment in marketing and inventory.
5. **Consumer Segment Dominates** — The Consumer segment drives the most revenue; Corporate and Home Office segments present growth opportunities.

---

## ✅ Final Data Quality Confirmation

After cleaning, the dataset meets the following standards:

- ✅ Zero missing values across all columns
- ✅ Correct data types (`datetime`, `float64`, `category`)
- ✅ No duplicate records
- ✅ Standardized categorical text (lowercase, trimmed)
- ✅ Outliers addressed via IQR winsorization
- ✅ Ready for advanced modeling or BI reporting

---

## 🚀 How to Run

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/ManikantaVejandla04/superstore-eda.git

# 2. Navigate to the project folder
cd superstore-eda

# 3. Launch Jupyter Notebook
jupyter notebook EDA_Project.ipynb
```

> Make sure `SuperstoreData.csv` is in the same directory as the notebook before running.

---

## 👤 Author

**V. Manikanta**
Data Analyst | Innomatics Research Labs

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/manikanta1015)
[![Email](https://img.shields.io/badge/Email-Contact-red?logo=gmail)](mailto:vmanikanta1015@gmail.com)

---

## 📄 License

This project is intended for educational and portfolio purposes.
