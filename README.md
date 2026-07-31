# Bird Migration Prediction — Group C

<br>
<p align="center">
  <strong>Report submitted by:</strong>
</p>
<p align="center">
  <strong>B. JASVANTH</strong><br>
  Lendi Institute of Engineering and Technology, Vizianagaram<br>
  jasvanth1063@gmail.com
</p>
<p align="center">
  <strong>JAYANT PANDEY</strong><br>
  Chandigarh University<br>
  jayantkvmau3@gmail.com
</p>
<p align="center">
  <em>For the successful completion of the internship as</em><br>
  <strong>Summer (Data Science) Interns 2026</strong><br>
  <strong>[Tenure: 7 weeks]</strong>
</p>
<p align="center">
  <em>Under the supervision of</em><br><br>
  <strong>Mr. Samyabrata Roy</strong><br>
  Associate Software Developer<br>
  IDEAS - Institute of Data Engineering, Analytics and Science Foundation,<br>
  Technology Innovation Hub, Indian Statistical Institute, Kolkata<br>
  sroy@ideas-tih.org
</p>
<br>
<p align="center">
  <strong>Report submitted to:</strong><br><br>
  <strong>
  IDEAS - Institute of Data Engineering, Analytics and Science Foundation,<br>
  Technology Innovation Hub, Indian Statistical Institute,<br>
  Kolkata, West Bengal, India
  </strong>
</p>

---

# IDEAS-TIH Summer Internship Program 2026

This repository contains the complete project work completed by **B. Jasvanth** and **Jayant Pandey** as part of the **Summer Internship Program 2026** under **IDEAS - Technology Innovation Hub, Indian Statistical Institute, Kolkata**.

---

# Project Details

## Project Title

**Interpretable Machine Learning Application in Bird Migration Trajectory Analysis Using GPS Data**

---

## Project Category

- Machine Learning Project
- Data Analysis Project
- Interpretable Project

---

## Problem Statement

Bird migration is one of the most complex phenomena in ecology, involving billions of birds travelling thousands of kilometres annually between breeding and wintering grounds. This project addresses the problem of **predicting which geographic migration zone a bird will occupy next**, given its recent GPS telemetry history.

The task is framed as **multi-class zone classification** — predicting a discrete geographic zone label rather than a continuous coordinate — using an end-to-end interpretable machine learning pipeline emphasising **correctness, reproducibility, and interpretability** over research novelty.

---

## Dataset

- **Source:** MoveBank GPS tracking — White Stork migration
- **Records:** 61,920 GPS fixes across 3 birds
- **Period:** 15 August 2013 – 30 April 2014 (258 days — full annual migration cycle)
- **Raw features:** latitude, longitude, altitude, speed\_2d, direction, date\_time, bird\_name, device\_info\_serial

---

## Pipeline

| Phase | Description |
|---|---|
| 1 | Dataset Understanding |
| 2 | Data Cleaning |
| 3 | Exploratory Data Analysis |
| 4 | Feature Engineering |
| 5 | Migration Zone Discovery |
| 6 | Sequence Dataset Construction |
| 7 | Model Development |
| 8 | Model Evaluation |
| 9 | Model Interpretation |

---

## Key Results

| Metric | Value |
|---|---|
| Best Model | Decision Tree (max\_depth=8) |
| Mean Accuracy (5-fold TimeSeriesSplit) | 99.85% |
| Mean F1-macro | 99.83% |
| ROC-AUC (valid folds) | 0.9973 |
| Migration Zones Discovered (K-Means, k=3) | Netherlands · North Africa · West Africa |
| Silhouette Score (k=3) | 0.8296 |
| Davies-Bouldin Index (k=3) | 0.2266 |
| Calinski-Harabasz Score | 1,115,121.14 |
| Total sequence windows constructed | 61,905 |
| Features per window | 40 (8 per timestep × 5 timesteps) |
| Total misclassifications (held-out) | 17 / 10,317 (0.16%) |

---

## Data Integrity Fixes Applied

1. **Merge collision** — `bird_migration_clustered.csv` had 166 duplicate rows caused by `merge(on='date_time')` without keying on `bird_name`. Fixed at root cause. Final shape: 61,920 rows, 0 duplicates.
2. **Missing coordinate scaling** — K-Means was fit on unscaled radian coordinates. `StandardScaler` added before fitting.
3. **Non-reproducible sampling** — Silhouette sample used no random seed. Fixed to `RandomState(42)`.

---

## Repository Structure

```
Group-C/
│
├── data/
│   ├── raw/
│   │   └── bird_migration_raw.csv
│   └── processed/
│       ├── bird_migration_cleaned.csv
│       ├── bird_migration_features.csv
│       ├── bird_migration_clustered.csv
│       └── bird_migration_sequence.csv
│
├── notebooks/
│   ├── Data_Cleaning_Feature_Engineering.ipynb
│   ├── Exploratory_Data_Analysis.ipynb
│   ├── Migration_Zone_Discovery.ipynb
│   ├── Sequence_Dataset_Construction.ipynb
│   ├── Model_Development.ipynb
│   ├── Model_Evaluation.ipynb
│   └── Model Interpretation.ipynb
│
├── output/
│   ├── html_charts/
│   │   ├── charts_02_04/                      <!-- Data Cleaning + Feature Engineering -->
│   │   │   ├── accelaration_boxplot.jpeg
│   │   │   ├── bird_speed_distribution_0_5ms.png
│   │   │   ├── Figure_01_Bird_Speed_Distribution_Full.png
│   │   │   ├── haversine_boxplot.jpeg
│   │   │   ├── time_delta(boxplots).jpeg
│   │   │   └── turning_rate(boxplot).jpeg
│   │   ├── charts_03/                         <!-- Exploratory Data Analysis -->
│   │   │   ├── eda_1_overview.html
│   │   │   ├── eda_2_histograms.html
│   │   │   ├── eda_3_scatter.html
│   │   │   ├── eda_4_trajectory.html
│   │   │   ├── eda_5_correlation.html
│   │   │   ├── eda_6_boxplots.html
│   │   │   ├── eda_7_temporal.html
│   │   │   ├── eda_8_geomap.html
│   │   │   ├── eda_9_seasons.html
│   │   │   ├── eda_10_kde.html
│   │   │   ├── eda_11_birdwise.html
│   │   │   ├── eda_12_pairplot.html
│   │   │   ├── eda_13_missing.html
│   │   │   ├── eda_birdwise_maps.html
│   │   │   ├── eda_daily_activity.html
│   │   │   └── phase3_kmeans_elbow.html
│   │   ├── charts_05/                         <!-- Migration Zone Discovery -->
│   │   │   ├── phase5_cluster_map.html
│   │   │   ├── phase5_evaluation_metrics.html
│   │   │   └── phase5_per_point_silhouette.html
│   │   ├── charts_06/                         <!-- Sequence Dataset Construction -->
│   │   │   ├── phase6_target_distribution.html
│   │   │   ├── phase6_target_per_bird.html
│   │   │   ├── phase6_timeline.html
│   │   │   └── phase6_windows_per_bird.html
│   │   ├── charts_07/                         <!-- Model Development -->
│   │   │   ├── phase7_model_comparison.html
│   │   │   └── phase7_train_vs_test.html
│   │   ├── charts_08/                         <!-- Model Evaluation -->
│   │   │   ├── phase8_clustering_metrics.html
│   │   │   ├── phase8_confusion_matrix.html
│   │   │   ├── phase8_metrics_per_fold.html
│   │   │   └── phase8_metrics_summary.html
│   │   └── charts_09/                         <!-- Model Interpretation -->
│   │       ├── phase9_confusion_matrix.html
│   │       ├── phase9_feature_importance.html
│   │       ├── phase9_shap_global_importance.png
│   │       ├── phase9_shap_summary_class0.png
│   │       ├── phase9_shap_summary_class1.png
│   │       └── phase9_shap_summary_class2.png
│   └── models/
│       ├── best_model.pkl
│       └── feature_cols.pkl
│
├── produced_reports/
│   ├── cv_results.csv
│   ├── interpretation_report.txt
│   └── evaluation_report.txt
│
├── index.html
└── README.md
```
# To Run Visuals 
1.open index.html via code editor
2.now after cloning this repository run this along the terminl.
3.click on the phase wise visual you want (plotly initialized).
---

## How to Run

1. Clone this repository
2. Upload `bird_migration.csv` to `/content/` in visual studio code
3. Run notebooks strictly in order from `Data_Cleaning_Feature_Engineering.ipynb` through `Model Interpretation`.
4. Run all cells top to bottom
---

## Tech Stack

- Python 3.10+
- pandas, numpy, scikit-learn, xgboost, shap
- plotly (all charts — 100% interactive HTML)
- joblib (model serialisation)
---

## Dataset

- **Source:** MoveBank GPS tracking — White Stork migration
- **Records:** 61,920 GPS readings across 3 birds
- **Period:** August 2013 – April 2014 (258 days)
- **Features:** latitude, longitude, altitude, speed\_2d, direction, timestamp, bird\_name
---

*Bird Migration GPS Tracking — Interpretable ML Pipeline | ISI Kolkata IDEAS Internship 2026 | Group C*
Jayanth pandey(Chandigarh university) &
B. Jasvanth (Lendi Institute of Engineering and Technology)*
