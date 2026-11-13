# craigslist-used-car-price-prediction

# Used Vehicle Price Prediction & Market Valuation System

**Course:** CDS4003 – End-to-End Data Science Project  
**Live Streamlit Application:** [Deployed Streamlit App Link Here]  
**Project Status:** Stages 1–4 Completed (Data Understanding, Cleaning, EDA, Feature Engineering & Baseline Modeling)

---

## 1. Business Problem Formulation
In the secondary automotive market, inconsistent pricing across online classified platforms creates significant friction for both buyers and dealerships. Sellers frequently overprice or underprice inventory due to subjective valuation, while buyers struggle to assess fair market value across varying vehicle ages, mileage, conditions, and regional markets.

* **Business Objective:** Develop an end-to-end machine learning valuation system that predicts fair market asking prices for used vehicles using structured listing attributes.
* **Target Stakeholders:** Independent used-car dealerships, online marketplace platforms, and private vehicle buyers/sellers.
* **Success Criteria:** Achieve strong predictive accuracy ($R^2 > 0.80$) with interpretable key pricing drivers, deployed as an interactive web application.

---

## 3. Dataset Source, License & Schema
* **Dataset:** Craigslist Used Cars & Trucks Dataset (`vehicles.csv`)
* **Source:** [Kaggle – Austin Reese Craigslist Vehicles Dataset](https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data)
* **License:** CC0 1.0 Universal (Public Domain Dedication)
* **Raw Dimensions:** 295,451 rows × 41 columns (meets the 200,000+ rows and 20+ columns requirement)
* **Cleaned Dimensions:** 191,840 rows × 23 columns (64.93% retention after systematic quality filtering)

> **Note on Large Files:** Due to GitHub's file size limits, the raw and cleaned CSV datasets are excluded from this repository. Use the Kaggle setup cell in `notebooks/01_data_understanding_and_cleaning.ipynb` to download and reproduce `vehicles_cleaned.csv` automatically.

---

## 4. Repository Structure
```text
├── notebooks/
│   ├── 01_data_understanding_and_cleaning.ipynb   # Stage 2 & 3: Quality audit, deduplication, outlier & null handling
│   └── 03_eda_and_modeling.ipynb                  # Stage 4 & 5: EDA visualizations, feature engineering & baseline RF model
├── outputs/
│   └── figures/
│       ├── fig_3_1_missing_values_cleaned.png     # Post-cleaning missing value profile
│       ├── fig_3_2_price_before_after.png         # Asking price distribution before & after cleaning
│       ├── fig_4_1_price_distribution.png         # Cleaned price distribution (up to 99th percentile)
│       ├── fig_4_2_top_manufacturers.png          # Market share & median prices of top 10 brands
│       ├── fig_4_3_depreciation_condition.png     # Vehicle age depreciation & condition boxplots
│       ├── fig_4_4_correlation_heatmap.png        # Feature correlation matrix
│       └── fig_4_5_feature_importance.png         # Top 10 Random Forest feature importances
├── app/                                           # Streamlit web application (Upcoming - Stage 7)
├── requirements.txt                               # Python dependencies
└── README.md                                      # Project documentation
```

---

## 5. How to Run the Project Locally or in Google Colab
1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```
2. **Install required libraries:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Execute Notebooks in Sequence:**
   * Run `notebooks/01_data_understanding_and_cleaning.ipynb` to download the Kaggle dataset, execute the data cleaning pipeline, and generate `vehicles_cleaned.csv`.
   * Run `notebooks/03_eda_and_modeling.ipynb` to generate all EDA charts, engineer features (`vehicle_age`, `mileage_per_year`), and train the baseline Random Forest model.

---

## 6. Key Results & Progress Summary

### Data Cleaning Summary (Stage 3)
* **Columns Dropped (18):** Removed 100% null columns (`county`, `size`), high-null metadata (`monthly_payment`, `other_attributes`), and non-predictive identifiers/URLs (`id`, `VIN`, `url`, `description`).
* **Duplicates Removed:** Eliminated **86,974** duplicate vehicle listings across core vehicle attributes.
* **Outliers & Invalid Records Filtered:** Restricted `price` to `$500–$150,000`, `year` to `1980–2026`, and `odometer` to `1–500,000 miles`.

### Exploratory Data Analysis & Baseline Modeling (Stages 4 & 5)
* **Key Market Insights:** Asking prices exhibit a right-skewed distribution (median: **$11,995**). Vehicles experience steep depreciation during their first 10–15 years, while `odometer` ($r = -0.48$) and `vehicle_age` ($r = -0.40$) show the strongest negative correlations with price.
* **Engineered Features:** `vehicle_age` (`2026 - year`) and `mileage_per_year` (`odometer / (vehicle_age + 1)`).
* **Baseline Model (Random Forest Regressor):**
  * **$R^2$ Score:** `0.8144`
  * **Mean Absolute Error (MAE):** `$3,907.96`
  * **Root Mean Squared Error (RMSE):** `$6,807.55`
  * **Top Predictors:** `vehicle_age`, `odometer`, `year`, and `cylinders_num`.

---

## 7. Next Milestones
* [ ] **Stage 5 & 6 (Week 13):** Compare multiple models (Random Forest, XGBoost/Gradient Boosting, Ridge Regression) and perform hyperparameter tuning (`RandomizedSearchCV`).
* [ ] **Stage 7 (Week 14):** Build and deploy the interactive valuation web app on Streamlit Community Cloud.
