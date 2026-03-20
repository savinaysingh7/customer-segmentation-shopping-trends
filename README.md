# 🛍️ Customer Segmentation Using Shopping Trends

> Segment 3,900 retail customers into 4 behavioral clusters using K-Means — and turn segments into strategy.

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/pandas-2.2.2-150458?logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/numpy-1.26.4-013243?logo=numpy&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-1.4.2-F7931E?logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/matplotlib-3.8.4-11557C" />
  <img src="https://img.shields.io/badge/seaborn-0.13.2-4C72B0" />
  <img src="https://img.shields.io/badge/plotly-latest-3F4F75?logo=plotly&logoColor=white" />
  <img src="https://img.shields.io/badge/Jupyter-1.0.0-F37626?logo=jupyter&logoColor=white" />
  <img src="https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/Clusters-4-brightgreen" />
  <img src="https://img.shields.io/badge/Records-3%2C900-lightgrey" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

<p align="center">
  <a href="https://github.com/savinaysingh7/customer-segmentation-shopping-trends">
    <img src="https://img.shields.io/badge/GitHub-View%20Repository-181717?logo=github&logoColor=white" />
  </a>
  &nbsp;
  <a href="https://www.linkedin.com/posts/savinaysingh_datascience-customersegmentation-machinelearning-activity-7350401903760920577-Z3lL">
    <img src="https://img.shields.io/badge/LinkedIn-Project%20Post-0A66C2?logo=linkedin&logoColor=white" />
  </a>
</p>

---

## 📋 Table of Contents

- [🌟 Overview](#-overview)
- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [📊 Dataset](#-dataset)
- [📁 Project Structure](#-project-structure)
- [⚡ Quick Start](#-quick-start)
- [🔄 Pipeline Walkthrough](#-pipeline-walkthrough)
- [🔍 Exploratory Data Analysis](#-exploratory-data-analysis)
- [🛠️ Feature Engineering](#️-feature-engineering)
- [🤖 Clustering & Segments](#-clustering--segments)
- [📈 Power BI Dashboard](#-power-bi-dashboard)
- [📖 Usage Examples](#-usage-examples)
- [🚀 Deployment & Reporting](#-deployment--reporting)
- [👥 Team](#-team)
- [📄 License](#-license)

---

## 🌟 Overview

This project builds an **end-to-end unsupervised machine learning pipeline** to segment retail customers based on their shopping behavior. Starting from a raw 3,900-row dataset of US consumer transactions, the pipeline cleans data, engineers 7 business-relevant features, and applies **K-Means clustering (k=4)** to identify four distinct customer personas.

The output — a labeled dataset, an interactive Power BI dashboard, and a 7-page business report — is designed to directly inform **targeted marketing campaigns, subscription upsell strategies, and seasonal promotions** for a retail or e-commerce business.

**Target audience:** Data science teams, retail analysts, and marketing strategists looking to move from raw transaction data to actionable customer intelligence.

---

## ✨ Features

- 🧹 **Automated data validation** — detects and reports missing values, duplicate rows, and outliers at pipeline entry; zero data quality issues found in source data
- 📐 **IQR-based outlier capping** — `Purchase Amount (USD)` capped at the 95th percentile to prevent high-spend records from distorting cluster centroids
- ⚙️ **Modular `ColumnTransformer` pipeline** — `StandardScaler` on numerics and `OneHotEncoder` on all categoricals, reapplied consistently in both preprocessing and clustering notebooks
- 💰 **Customer Lifetime Value (CLV) proxy** — engineered as `Purchase Amount × Previous Purchases`; ranges from near-zero to $5,000, enabling revenue-based segmentation
- 📅 **Purchase frequency scoring** — converts text labels (Weekly → 7, Annually → 1) into an ordered numeric scale for direct use in clustering
- 🌦️ **Seasonal purchase flagging** — `Winter_Spring_Buyer` binary feature captures the strong seasonal split observed in EDA (~50% of all purchases in Winter/Spring)
- 🏷️ **Discount sensitivity detection** — identifies the 43% of customers who consistently combine `Discount Applied=Yes` AND `Promo Code Used=Yes`
- 📊 **Elbow curve + silhouette analysis** — k=4 selected using both methods, not just by assumption
- 🔵 **PCA 2D cluster visualization** — projects high-dimensional encoded features to 2D for interpretable scatter plots of all four segments
- 📉 **Plotly interactive cluster profiles** — bar and scatter charts per cluster rendered directly in the clustering notebook
- 🗺️ **Geographic analysis** — purchase behavior mapped across all represented US states in EDA
- 📋 **Power BI dashboard** — single-page interactive report with KPI cards, cluster-aware categorical charts, slicers (Cluster / Gender / Season / Subscription), and a US state map visual
- 📄 **PDF business report** — 7-page human-readable summary with cluster personas, strategic recommendations, and methodology overview

---

## 🛠️ Tech Stack

| Category | Library / Tool | Version | Purpose |
|----------|---------------|---------|---------|
| Language | Python | 3.8+ | Core pipeline language |
| Data manipulation | pandas | 2.2.2 | DataFrame operations, CSV I/O |
| Numerical computing | numpy | 1.26.4 | Array operations, percentile calculations |
| Visualization | matplotlib | 3.8.4 | Static plots in EDA and feature engineering |
| Visualization | seaborn | 0.13.2 | Statistical plots — pair plots, heatmaps, box plots |
| Visualization | plotly | latest* | Interactive cluster profile charts in clustering notebook |
| Machine learning | scikit-learn | 1.4.2 | KMeans, PCA, StandardScaler, OneHotEncoder, ColumnTransformer |
| Spreadsheet I/O | openpyxl | 3.1.2 | Excel export support |
| Notebook environment | Jupyter | 1.0.0 | Interactive development environment |
| BI reporting | Power BI Desktop | — | Interactive dashboard (`customer_seg_dashboard.pbix`) |
| Report format | PDF | — | Business summary report |

> ⚠️ `plotly` is **not listed in `requirements.txt`** but is imported in `clustering_shopping_trends.ipynb`. Install it manually: `pip install plotly`

---

## 📊 Dataset

**File:** `shopping_trends.csv` — 3,900 rows × 19 columns — no missing values — no duplicate rows

| Column | Type | Values / Range | Notes |
|--------|------|---------------|-------|
| `Customer ID` | int | 1–3900 | Dropped during preprocessing |
| `Age` | int | 18–70 (mean: 44.1) | Used as-is and binned into `Age_Group` |
| `Gender` | str | Male (68.0%), Female (32.0%) | One-hot encoded |
| `Item Purchased` | str | 45+ distinct items | One-hot encoded |
| `Category` | str | Clothing, Accessories, Footwear, Outerwear | One-hot encoded; used for `Dominant_Category` |
| `Purchase Amount (USD)` | float | $20–$100 (mean: $59.80) | Outlier-capped at 95th percentile |
| `Location` | str | US states | One-hot encoded; geographic EDA |
| `Size` | str | S, M, L, XL | One-hot encoded |
| `Color` | str | 22+ colors | One-hot encoded |
| `Season` | str | Winter, Spring, Summer, Fall | Source of `Winter_Spring_Buyer` flag |
| `Review Rating` | float | 2.5–5.0 (mean: 3.75) | Binned into `Review_Rating_Category` |
| `Subscription Status` | str | Yes (27.0%), No (73.0%) | Key cluster differentiator |
| `Payment Method` | str | Cash, Credit Card, Debit Card, PayPal, Venmo, Bank Transfer | One-hot encoded |
| `Shipping Type` | str | Express, Free Shipping, Next Day Air, Standard, Store Pickup, 2-Day Shipping | One-hot encoded |
| `Discount Applied` | str | Yes (43.0%), No (57.0%) | Component of `Discount_Sensitivity` |
| `Promo Code Used` | str | Yes / No | Component of `Discount_Sensitivity` |
| `Previous Purchases` | int | Varies | Used in CLV calculation |
| `Preferred Payment Method` | str | Same values as Payment Method | One-hot encoded |
| `Frequency of Purchases` | str | Weekly, Fortnightly, Monthly, Bi-Weekly, Quarterly, Every 3 Months, Annually | Mapped to `Purchase_Frequency_Score` |

---

## 📁 Project Structure

```
customer-segmentation-shopping-trends/
│
├── README.md                                         ← Project documentation
├── requirements.txt                                  ← Pinned Python dependencies
├── Links.txt                                         ← GitHub & LinkedIn links
│
├── Data (CSV pipeline)
│   ├── shopping_trends.csv                           ← Raw source dataset (3,900 × 19)
│   ├── preprocessed_shopping_trends.csv              ← After scaling + one-hot encoding
│   ├── shopping_trends_engineered.csv                ← After CLV, freq score, flags, etc.
│   └── shopping_trends_clustered.csv                 ← Final output with Cluster column
│
├── Notebooks (execute in this sequence)
│   ├── preprocess_shopping_trends.ipynb              ← Step 1: clean & encode
│   ├── eda_shopping_trends.ipynb                     ← Step 2: explore & visualize
│   ├── feature_engineering_shopping_trends.ipynb    ← Step 3: engineer features
│   └── clustering_shopping_trends.ipynb              ← Step 4: cluster & profile
│
└── Reporting
    ├── customer_seg_dashboard.pbix                   ← Power BI interactive dashboard
    └── Customer Segmentation for Business Insights.pdf  ← 7-page stakeholder report
```

---

## ⚡ Quick Start

### Prerequisites

```
Python  >= 3.8
pip     >= 21.0
Jupyter Notebook or JupyterLab
Power BI Desktop (optional — for .pbix dashboard only)
```

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/savinaysingh7/customer-segmentation-shopping-trends.git
cd customer-segmentation-shopping-trends

# 2. Create and activate a virtual environment
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate

# 3. Install pinned dependencies
pip install -r requirements.txt

# 4. Install plotly (used in clustering notebook, missing from requirements.txt)
pip install plotly

# 5. Launch Jupyter
jupyter notebook
```

### Notebook Execution Order

```
1. preprocess_shopping_trends.ipynb          → produces preprocessed_shopping_trends.csv
2. eda_shopping_trends.ipynb                 → produces visualizations (no new CSV output)
3. feature_engineering_shopping_trends.ipynb → produces shopping_trends_engineered.csv
4. clustering_shopping_trends.ipynb          → produces shopping_trends_clustered.csv
```

> ⚠️ **Dependency note:** The clustering notebook loads `shopping_trends_engineered.csv` — run the feature engineering notebook first.
>
> ⚠️ **Input note:** The feature engineering notebook reads from the **raw** `shopping_trends.csv`, not from the preprocessed output.

---

## 🔄 Pipeline Walkthrough

### Step 1 — `preprocess_shopping_trends.ipynb`

| Action | Detail |
|--------|--------|
| Load | `shopping_trends.csv` (3,900 × 19) |
| Drop | `Customer ID` — not a behavioral feature |
| Validate | 0 missing values confirmed, 0 duplicate rows confirmed |
| Outlier treatment | `Purchase Amount (USD)` capped at 95th percentile using IQR logic |
| Encode | `ColumnTransformer`: `StandardScaler` on numeric cols, `OneHotEncoder` on categorical cols |
| Save | `preprocessed_shopping_trends.csv` |

### Step 2 — `eda_shopping_trends.ipynb`

| Analysis Layer | Charts |
|----------------|--------|
| Univariate | Histograms and box plots for Age, Purchase Amount, Review Rating, Previous Purchases |
| Categorical | Bar charts for Gender, Category, Season, Subscription Status, Shipping Type, Payment Method |
| Bivariate | Pair plot (Age × Purchase × Rating × Prev Purchases), Pearson correlation heatmap |
| Group comparison | Box plots of Purchase Amount split by Category, Gender, Location |
| Crosstab heatmaps | Season × Category, Gender × Season, Payment Method × Shipping Type |
| Geographic | Purchase amount and count aggregated by US state |

### Step 3 — `feature_engineering_shopping_trends.ipynb`

Loads `shopping_trends.csv` (raw) and appends 7 new columns. See [Feature Engineering](#️-feature-engineering) below.

### Step 4 — `clustering_shopping_trends.ipynb`

```
Load shopping_trends_engineered.csv
       ↓
Re-apply ColumnTransformer (StandardScaler + OneHotEncoder)
       ↓
Elbow Curve (k=1..10) + Silhouette Score analysis  →  k=4 selected
       ↓
KMeans(n_clusters=4, random_state=42).fit()
       ↓
PCA(n_components=2)  →  2D scatter plot of all 4 clusters
       ↓
Plotly interactive bar charts profiling each cluster
       ↓
Append Cluster column  →  save shopping_trends_clustered.csv
```

---

## 🔍 Exploratory Data Analysis

### Key Statistics

| Metric | Value |
|--------|-------|
| Total customers | 3,900 |
| Age range | 18–70 (mean: **44.1**) |
| Purchase amount range | $20–$100 (mean: **$59.80**) |
| Review rating range | 2.5–5.0 (mean: **3.75**) |
| Gender split | **68.0% Male** / 32.0% Female |
| Subscribed | **27.0%** (1,053 customers) |
| Discount applied | **43.0%** (1,677 transactions) |
| Top category | **Clothing** (~44.5%) |
| Second category | **Accessories** (~31.8%) |
| Peak seasons | **Winter & Spring** (~50% combined) |

### EDA Findings That Shaped Feature Engineering

- **Discount + Promo are tightly correlated** — combined into the `Discount_Sensitivity` binary flag
- **~50% of purchases concentrate in Winter/Spring** — motivated the `Winter_Spring_Buyer` flag
- **Previous Purchases × Amount form a strong interaction** — their product became the `CLV` feature
- **Frequency labels are naturally ordinal** — the 7-level field maps cleanly to an integer 1–7 score
- **Review ratings are narrowly clustered between 3.0–5.0** — justified the three-tier binning

---

## 🛠️ Feature Engineering

```python
# Customer Lifetime Value proxy
df['CLV'] = df['Purchase Amount (USD)'] * df['Previous Purchases']
# Range: near-$0 to $5,000 | Mean: ~$1,518

# Purchase Frequency Score — ordinal encoding
freq_map = {
    'Weekly': 7, 'Fortnightly': 6, 'Monthly': 5,
    'Bi-Weekly': 4, 'Quarterly': 3,
    'Every 3 Months': 2, 'Annually': 1
}
df['Purchase_Frequency_Score'] = df['Frequency of Purchases'].map(freq_map)
# Range: 1–7 | Mean: ~3.95

# Age Group binning
df['Age_Group'] = pd.cut(df['Age'], bins=[0, 30, 55, 100],
                          labels=['Young', 'Middle-Aged', 'Senior'])

# Discount Sensitivity: both discount AND promo used
df['Discount_Sensitivity'] = (
    (df['Discount Applied'] == 'Yes') & (df['Promo Code Used'] == 'Yes')
).astype(int)
# ~43% = 1

# Seasonal flag
df['Winter_Spring_Buyer'] = df['Season'].isin(['Winter', 'Spring']).astype(int)
# ~50% = 1

# Review rating tier
df['Review_Rating_Category'] = pd.cut(df['Review Rating'],
    bins=[0, 3.0, 4.0, 5.0], labels=['Low', 'Medium', 'High'])
```

The 7th feature, `Dominant_Category`, carries each customer's `Category` field value forward as a named label.

---

## 🤖 Clustering & Segments

**Algorithm:** K-Means &nbsp;|&nbsp; **k=4** selected via elbow curve + silhouette score

### Cluster Distribution

| Cluster | Label | Count | % of Dataset |
|---------|-------|-------|--------------|
| 0 | Seasonal Female Shoppers | 914 | 23.4% |
| 1 | Male Bargain Hunters | 1,333 | 34.2% |
| 2 | High-Value Loyalists | 760 | 19.5% |
| 3 | Non-Seasonal Female Shoppers | 893 | 22.9% |

---

### 🔵 Cluster 0 — Seasonal Female Shoppers

| Metric | Value |
|--------|-------|
| Mean CLV | $1,116 |
| Mean Purchase Amount | $54.60 |
| Mean Age | 43.4 |
| Mean Previous Purchases | 21.9 |
| Gender | 56.1% Female |
| Season | **100% Winter / Spring** |
| Subscription Rate | **0.0%** |
| Discount Sensitivity | **0%** |

**Business Action:** Target with Winter/Spring launch campaigns and new-arrival lookbooks. Not discount-driven — curated product storytelling outperforms promotions here. Zero subscriptions = top target for a seasonal early-access subscription offer.

---

### 🟠 Cluster 1 — Male Bargain Hunters *(Largest Cluster)*

| Metric | Value |
|--------|-------|
| Mean CLV | $1,068 |
| Mean Purchase Amount | $53.60 |
| Mean Age | 43.9 |
| Mean Previous Purchases | 21.8 |
| Gender | **100% Male** |
| Season | 51.2% Winter/Spring |
| Subscription Rate | **63.6%** |
| Discount Sensitivity | **100%** |

**Business Action:** Every customer uses discounts + promos — avoid open margin erosion with blanket sales. Reward loyalty through tiered member-exclusive deals instead. With 63.6% already subscribed, this is the highest-engagement segment for push and email campaigns.

---

### 🟢 Cluster 2 — High-Value Loyalists ⭐ *(Priority Segment)*

| Metric | Value |
|--------|-------|
| Mean CLV | **$3,341** |
| Mean Purchase Amount | **$82.30** |
| Mean Age | 45.2 |
| Mean Previous Purchases | **41.0** |
| Gender | 70.7% Male |
| Season | 49.1% Winter/Spring |
| Subscription Rate | 27.0% |
| Discount Sensitivity | 45.3% |

**Business Action:** CLV is 3× higher than any other cluster. Despite 41 previous purchases per customer, only 27% are subscribed — this is the highest-ROI conversion opportunity in the dataset. Invest in VIP programs and premium tier subscriptions targeted at this group.

---

### 🔴 Cluster 3 — Non-Seasonal Female Shoppers

| Metric | Value |
|--------|-------|
| Mean CLV | $1,049 |
| Mean Purchase Amount | $55.10 |
| Mean Age | 44.1 |
| Mean Previous Purchases | 20.8 |
| Gender | 57.3% Female |
| Season | **0% Winter/Spring** (100% Summer/Fall) |
| Subscription Rate | **0.0%** |
| Discount Sensitivity | **0%** |

**Business Action:** The Summer/Fall counterpart to Cluster 0. Not discount-driven; respond to lifestyle and aesthetic content. Zero subscriptions — test Summer-launch subscription incentives in Q2/Q3 to begin building retention.

---

## 📈 Power BI Dashboard

**File:** `customer_seg_dashboard.pbix` — open with [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)

| Element | Description |
|---------|-------------|
| KPI Cards | Total customers, mean CLV, mean purchase amount for the filtered view |
| Bar charts | Cluster breakdowns of Category, Gender, Season, and Subscription Status |
| Slicers | Filter entire report by Cluster (0–3), Gender, Season, Subscription Status |
| Map visual | Customer geographic distribution across US states |

> If prompted on open, reconnect the data source to your local `shopping_trends_clustered.csv`.

---

## 📖 Usage Examples

### Inspect clustered output

```python
import pandas as pd

df = pd.read_csv("shopping_trends_clustered.csv")

# Cluster distribution
print(df["Cluster"].value_counts().sort_index())
# 0     914
# 1    1333
# 2     760
# 3     893

# Mean CLV and Purchase Amount per cluster
print(df.groupby("Cluster")[["CLV", "Purchase Amount (USD)"]].mean().round(2))
```

### Find high-value unsubscribed customers (subscription upsell)

```python
upsell = df[(df["Cluster"] == 2) & (df["Subscription Status"] == "No")]
print(f"Upsell targets: {len(upsell)}, mean CLV: ${upsell['CLV'].mean():.0f}")
```

### Export a segment for a seasonal campaign

```python
campaign = df[
    (df["Cluster"] == 0) & (df["Season"].isin(["Winter", "Spring"]))
][["Age", "Gender", "Category", "CLV", "Cluster"]]
campaign.to_csv("cluster0_winter_spring_campaign.csv", index=False)
```

### Reproduce clustering from scratch

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA

df = pd.read_csv("shopping_trends_engineered.csv")

numeric_cols  = ["Age", "Purchase Amount (USD)", "Previous Purchases",
                 "CLV", "Purchase_Frequency_Score"]
cat_cols = ["Gender", "Category", "Season", "Subscription Status",
            "Discount Applied", "Promo Code Used",
            "Age_Group", "Review_Rating_Category", "Winter_Spring_Buyer"]

preprocessor = ColumnTransformer([
    ("num", StandardScaler(), numeric_cols),
    ("cat", OneHotEncoder(handle_unknown="ignore"), cat_cols)
])

X = preprocessor.fit_transform(df)
df["Cluster"] = KMeans(n_clusters=4, random_state=42, n_init=10).fit_predict(X)

coords = PCA(n_components=2).fit_transform(X)
df["PC1"], df["PC2"] = coords[:, 0], coords[:, 1]
```

---

## 🚀 Deployment & Reporting

### Re-execute all notebooks non-interactively

```bash
jupyter nbconvert --to notebook --execute preprocess_shopping_trends.ipynb
jupyter nbconvert --to notebook --execute feature_engineering_shopping_trends.ipynb
jupyter nbconvert --to notebook --execute clustering_shopping_trends.ipynb
```

> The EDA notebook (`eda_shopping_trends.ipynb`) produces visualizations only and does not need to be re-executed to regenerate the data pipeline outputs.

### Publish Power BI dashboard

1. Open `customer_seg_dashboard.pbix` in Power BI Desktop
2. Refresh the data source pointing to local `shopping_trends_clustered.csv`
3. **Home → Publish** to Power BI Service for browser-based sharing (requires Power BI Pro or Premium)

---

## 🙏 Acknowledgments

- **scikit-learn** — KMeans, PCA, ColumnTransformer, StandardScaler, OneHotEncoder implementations
- **seaborn** — pair plots, correlation heatmaps, and grouped box plots throughout EDA
- **plotly** — interactive cluster profiling charts in the clustering notebook
- **Power BI Desktop** — free business intelligence tool (Microsoft) used for the dashboard layer

---

## 📄 License

This repository does not currently include a `LICENSE` file. To open-source the project, add one via **GitHub → Add file → Create new file → `LICENSE`**:

| License | Best suited for |
|---------|----------------|
| MIT | Maximum permissiveness — anyone can use, modify, distribute |
| Apache-2.0 | Permissive + explicit patent grant — common for ML projects |
| GPL-3.0 | Copyleft — derivative works must also remain open-source |

---

<p align="center">
  <sub>Built with Python 3.8+ · scikit-learn 1.4.2 · pandas 2.2.2 · Power BI Desktop</sub>
</p>