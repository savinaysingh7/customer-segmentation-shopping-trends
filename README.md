
# 🛍️ Customer Segmentation Using Machine Learning

This project implements an end-to-end data science pipeline to segment retail customers based on their shopping behavior and demographics. The goal is to uncover meaningful customer segments for targeted marketing, loyalty campaigns, and business strategy.

---

## 📌 Table of Contents

* [Project Overview](#project-overview)
* [Problem Statement](#problem-statement)
* [Tools & Technologies](#tools--technologies)
* [Workflow / Project Flow](#workflow--project-flow)
* [Key Features](#key-features)
* [Power BI Dashboard](#power-bi-dashboard)
* [Results & Insights](#results--insights)
* [How to Use](#how-to-use)
* [Project Structure](#project-structure)
* [License](#license)

---

## 🚀 Project Overview

In this project, we analyzed a retail shopping dataset with 3,900+ transactions. We applied machine learning and business analytics to:

* Preprocess and clean data
* Perform exploratory data analysis (EDA)
* Engineer new features like CLV (Customer Lifetime Value)
* Apply clustering (K-Means) to find customer groups
* Visualize and interpret insights using Power BI

---

## 🎯 Problem Statement

Retail businesses often struggle to understand diverse customer behaviors. By grouping similar customers together, businesses can tailor offerings, increase retention, and boost sales. This project aims to:

* Identify **high-value customers**
* Find **discount-sensitive** or **seasonal** shoppers
* Enable **data-driven marketing decisions**

---

## 🛠️ Tools & Technologies

* **Python**: Core language for preprocessing, analysis, and ML
* **Pandas, NumPy**: Data manipulation
* **Matplotlib, Seaborn**: Visualization
* **Scikit-learn**: Clustering (K-Means), encoding, scaling
* **Power BI**: Dashboard for interactive data exploration
* **Jupyter Notebook**: Code notebooks and analysis workflow

---

## 📊 Workflow / Project Flow

```bash
graph TD
A[Raw Dataset: shopping_trends.csv]
B[Data Preprocessing]
C[Exploratory Data Analysis (EDA)]
D[Feature Engineering]
E[Clustering with K-Means]
F[Segment Profiling]
G[Power BI Dashboard]

A --> B --> C --> D --> E --> F --> G
```

### 🔁 Step-by-Step Breakdown:

1. **Preprocessing** (`preprocess_shopping_trends.ipynb`)

   * Removed non-informative IDs
   * Handled outliers and encoded categorical variables
   * Scaled numerical features for modeling

2. **EDA** (`eda_shopping_trends.ipynb`)

   * Analyzed demographics, spend patterns, reviews
   * Explored relationships between features
   * Identified spending trends and potential segments

3. **Feature Engineering** (`feature_engineering_shopping_trends.ipynb`)

   * Added CLV (Purchase Amount × Previous Purchases)
   * Created Age Groups, Discount Sensitivity flag, Frequency Score
   * Labeled Seasonal Buyers and Rating Levels

4. **Clustering** (`clustering_shopping_trends.ipynb`)

   * Used KMeans to segment customers into 4 groups
   * Evaluated clusters using silhouette score & elbow method
   * Interpreted segment characteristics: high-value, deal-seekers, seasonal shoppers

5. **Dashboard** (`customer_seg_dashboard.pbix`)

   * Interactive filters for cluster, gender, location
   * KPIs, CLV analysis, spending heatmaps
   * Segment-wise drill-downs

---

## ✅ Key Features

* 🧼 Clean and standardized dataset
* 🧠 Feature-rich customer profile modeling
* 📈 KMeans clustering with interpretability
* 📊 Business-ready Power BI dashboard
* 🔍 Actionable segment insights

---

## 📉 Power BI Dashboard

The Power BI dashboard provides:

* Cluster-wise performance (CLV, frequency, purchase amount)
* Demographic filters (Gender, Age Group, State)
* Purchase category breakdown
* Seasonal trends and discount usage

> 📁 File: `customer_seg_dashboard.pbix`
> 🔑 Available for preview if you have Power BI Desktop

---

## 🧠 Results & Insights

* **Cluster 2**: High CLV, frequent male shoppers — top priority for retention
* **Cluster 1**: Discount-loving, male-only group — respond well to deals
* **Cluster 0**: Female seasonal buyers (Winter/Spring) — not subscribed yet
* **Cluster 3**: Female Summer/Fall buyers — non-discount, non-subscribers

Business Recommendation: Customize promotions per cluster, build loyalty incentives for female segments, and reward high-value customers.

---

## 📂 Project Structure

```bash
├── shopping_trends.csv                     # Raw dataset
├── preprocess_shopping_trends.ipynb       # Data cleaning and encoding
├── eda_shopping_trends.ipynb              # Visual EDA
├── feature_engineering_shopping_trends.ipynb  # New features creation
├── clustering_shopping_trends.ipynb       # KMeans clustering & evaluation
├── customer_seg_dashboard.pbix            # Power BI dashboard
├── project_report.pdf                     # Final report (optional)
└── README.md                              # You're here!
```

---

## 🧪 How to Use

1. Clone this repository
2. Open the notebooks in Jupyter or VSCode
3. Follow the flow: preprocessing → EDA → feature engineering → clustering
4. Open `customer_seg_dashboard.pbix` using **Power BI Desktop** to explore visualizations

---

## 📜 License

This project is for educational use. You are free to fork and build upon it for academic or personal portfolios.

---
