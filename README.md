# Customer Segmentation Using Shopping Trends Data

This repository contains an end-to-end customer segmentation project built on a retail shopping dataset with 3,900 transactions. The project covers data preprocessing, exploratory data analysis, feature engineering, K-Means clustering, and business reporting through a Power BI dashboard and a PDF summary.

The workflow starts from `shopping_trends.csv`, creates intermediate analysis artifacts, and ends with `shopping_trends_clustered.csv`, where each record is assigned to one of four customer segments.

## Description

The goal of the project is to group customers by shopping behavior so the resulting segments can support more targeted marketing, retention, and merchandising decisions.

From the notebooks and generated outputs in this repository, the pipeline does the following:

- Cleans and encodes the raw shopping trends dataset.
- Explores customer patterns across demographics, category preferences, seasonality, and spending.
- Engineers segmentation-focused features such as a CLV proxy, purchase frequency score, age group, discount sensitivity, and seasonal flags.
- Builds a 4-cluster K-Means model on the engineered dataset.
- Publishes analysis artifacts for both technical review and business-facing reporting.

The committed outputs show:

- `shopping_trends.csv`: 3,900 rows and 19 columns.
- No missing values in the raw dataset.
- No duplicate rows in the raw dataset.
- `shopping_trends_clustered.csv`: 3,900 rows labeled with 4 clusters.

## Key Features

- End-to-end notebook workflow from raw data to clustered output.
- Separate preprocessing, EDA, feature engineering, and clustering stages.
- One-hot encoding and standardization for modeling-ready features.
- Engineered customer metrics including:
  - `CLV`
  - `Purchase_Frequency_Score`
  - `Age_Group`
  - `Discount_Sensitivity`
  - `Dominant_Category`
  - `Winter_Spring_Buyer`
  - `Review_Rating_Category`
- K-Means clustering with elbow-curve and silhouette-score inspection.
- PCA-based 2D visualization of customer segments.
- Power BI dashboard artifact for interactive business analysis.
- PDF report summarizing the project and business insights.

## Tech Stack

| Area | Tools |
| --- | --- |
| Language | Python |
| Analysis | pandas, numpy |
| Visualization | matplotlib, seaborn, plotly |
| Machine Learning | scikit-learn |
| Notebook Environment | Jupyter Notebook |
| BI / Reporting | Power BI Desktop, PDF |
| Data Storage | CSV |

The repository's `requirements.txt` includes:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `jupyter`
- `openpyxl`

Note: `clustering_shopping_trends.ipynb` imports `plotly.express`, but `plotly` is not currently listed in `requirements.txt`. Install it separately before running that notebook.

## Folder Structure

```text
customer-segmentation-shopping-trends/
|-- README.md
|-- requirements.txt
|-- Links.txt
|-- shopping_trends.csv
|-- preprocessed_shopping_trends.csv
|-- shopping_trends_engineered.csv
|-- shopping_trends_clustered.csv
|-- preprocess_shopping_trends.ipynb
|-- eda_shopping_trends.ipynb
|-- feature_engineering_shopping_trends.ipynb
|-- clustering_shopping_trends.ipynb
|-- customer_seg_dashboard.pbix
`-- Customer Segmentation for Business Insights.pdf
```

## Project Workflow

1. `preprocess_shopping_trends.ipynb`
   - Loads `shopping_trends.csv`
   - Removes `Customer ID`
   - Checks missing values and duplicates
   - Inspects outliers and caps `Purchase Amount (USD)` at the 95th percentile
   - Standardizes numeric columns and one-hot encodes categorical columns
   - Saves `preprocessed_shopping_trends.csv`

2. `eda_shopping_trends.ipynb`
   - Explores distributions and summary statistics
   - Generates histograms, box plots, pair plots, and correlation heatmaps
   - Studies relationships across gender, category, location, season, and purchase behavior

3. `feature_engineering_shopping_trends.ipynb`
   - Loads the raw dataset
   - Adds engineered features used for segmentation
   - Saves `shopping_trends_engineered.csv`

4. `clustering_shopping_trends.ipynb`
   - Loads `shopping_trends_engineered.csv`
   - Reapplies scaling and one-hot encoding for clustering
   - Compares cluster counts using elbow and silhouette methods
   - Fits K-Means with `n_clusters=4`
   - Adds a `Cluster` column
   - Saves `shopping_trends_clustered.csv`

5. `customer_seg_dashboard.pbix`
   - Provides the business-facing visualization layer in Power BI
   - The committed dashboard contains a single page with cards, categorical charts, slicers, and a map visual

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/savinaysingh7/customer-segmentation-shopping-trends.git
cd customer-segmentation-shopping-trends
```

### 2. Create and activate a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
pip install plotly
```

### 4. Optional tools

- Install Power BI Desktop to open `customer_seg_dashboard.pbix`.
- Use Jupyter Notebook or JupyterLab to run the notebooks interactively.

## Usage

### Run the notebook pipeline

Start Jupyter:

```bash
jupyter notebook
```

Recommended notebook order:

1. `preprocess_shopping_trends.ipynb`
2. `eda_shopping_trends.ipynb`
3. `feature_engineering_shopping_trends.ipynb`
4. `clustering_shopping_trends.ipynb`

This sequence gives you the full project flow from cleaning through segmentation. The clustering notebook depends on `shopping_trends_engineered.csv`, which is produced by the feature engineering notebook.

### Use the pre-generated outputs directly

If you only want to inspect the finished results, you can skip notebook execution and use these committed files directly:

- `preprocessed_shopping_trends.csv`
- `shopping_trends_engineered.csv`
- `shopping_trends_clustered.csv`
- `customer_seg_dashboard.pbix`
- `Customer Segmentation for Business Insights.pdf`

### Open the dashboard

Open `customer_seg_dashboard.pbix` with Power BI Desktop to explore the final dashboard interactively.

## Example Usage

Use the final clustered dataset in Python:

```python
import pandas as pd

df = pd.read_csv("shopping_trends_clustered.csv")

print(df["Cluster"].value_counts().sort_index())
print(df.groupby("Cluster")[["CLV", "Purchase Amount (USD)"]].mean().round(2))
```

Expected cluster counts from the committed output:

```text
Cluster
0     914
1    1333
2     760
3     893
```

Example questions you can answer with the final dataset:

- Which segment has the highest CLV?
- Which customers are most discount-sensitive?
- How do seasonality and gender vary across clusters?
- Which segments are most likely to benefit from loyalty or subscription campaigns?

## License

This repository does not currently include a standalone `LICENSE` file. If you want others to reuse, modify, or distribute the project with clear legal terms, add a license file such as MIT, Apache-2.0, or GPL-3.0.
