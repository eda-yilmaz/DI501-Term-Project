# DI 501 Term Project

## Climate-Driven Maize Yield Instability Across Global Climate Panels
### A Data-Driven Clustering Approach Using CY-Bench

**Author:** Eda Yilmaz | Department of Information Systems, Middle East Technical University

---

## Project Description

This project investigates subnational maize yield instability across global climate panels using the CY-Bench dataset (2001–2023). A key methodological contribution is the replacement of theory-based Köppen-Geiger climate zone classifications with data-driven k-means clustering on growing-season climate variables. Hemisphere-aware feature engineering ensures that heat stress and precipitation predictors reflect actual growing-season conditions.

Four research questions are explored:

- **RQ1:** Do subnational maize yield instability levels differ significantly across data-driven climate clusters?
- **RQ2:** Can engineered climate stress features predict annual deviations of maize yield from its long-term trend at the subnational level?
- **RQ3:** Are the predictive improvements over the naive baseline statistically significant?
- **RQ4:** Which climate features drive predictions, and are there non-linear threshold effects?

---

## Dataset

This project uses the [CY-Bench dataset](https://github.com/BigDataWUR/AgML-crop-yield-forecasting), a global benchmark for subnational crop yield forecasting covering 42 countries at the administrative unit level (2001–2023). After quality filtering, the working dataset contains **157,894 region-year observations across 38 countries**.

> Download the CY-Bench data and place it in the `data/` folder before running the notebooks.

---

## Repository Structure

```
DI501-Term-Project/
├── data/                                          <- CY-Bench dataset (download separately)
├── notebooks/
│   ├── step3_data_quality.ipynb                   <- Data quality checks
│   ├── step3_descriptive_stats_table.ipynb        <- Descriptive statistics
│   ├── step4_naive_baseline.ipynb                 <- Naive baseline (detrended yield = 0)
│   ├── step4b_koppen_models.ipynb                 <- Theory-based Köppen panel models
│   ├── step5_feature_selection.ipynb              <- VIF / multicollinearity analysis
│   ├── step5b_clustering.ipynb                    <- K-means clustering (k=3, 38 countries)
│   ├── step6_models.ipynb                         <- Decision Tree & Random Forest models
│   ├── step7_hyperparameter_tuning.ipynb          <- GridSearchCV tuning (5-fold CV)
│   ├── step8_statistical_comparison.ipynb         <- Wilcoxon signed-rank significance tests
│   ├── step8b_comparison.ipynb                    <- Köppen vs data-driven comparison figure
│   └── step9_interpretability.ipynb               <- Permutation importance & PDPs
├── reports/
│   ├── figures/                                   <- All generated figures
│   │   ├── fig_preclustering_distributions.png    <- Distribution check before clustering
│   │   ├── fig_preclustering_scatter.png          <- Raw feature space before clustering
│   │   ├── fig_clustering_global.png              <- K-means clusters (Fig. 1 in paper)
│   │   ├── fig_cv_by_cluster_global.png           <- Yield instability boxplot (Fig. 2)
│   │   ├── fig_koppen_vs_clusters_comparison.png  <- Model comparison (Fig. 3)
│   │   ├── fig_partial_dependence.png             <- Partial dependence plots (Fig. 4)
│   │   └── fig_cluster_world_map.png              <- World map of cluster assignments
│   └── DI501_Final_Paper.pdf                      <- IEEE-format final paper
├── requirements.txt                               <- Required Python packages
└── README.md                                      <- This file
```

---

## Methods Summary

| Step | Method | Key Result |
|---|---|---|
| Feature engineering | Hemisphere-aware growing-season windows | Heat stress days, precipitation (mm) |
| Feature selection | VIF analysis (4 → 2 features) | Dropped `tavg_jja` (VIF=130) and `cwb_deficit_gs` (VIF=80) |
| Yield detrending | OLS per region (min. 5 obs) | Detrended yield residuals |
| Clustering | K-means, k=3 (elbow + silhouette) | Semi-arid (9), Temperate (24), Tropical (5) countries |
| Cluster validation | Ward hierarchical robustness check | 37/38 countries identical assignment |
| Yield instability | Kruskal-Wallis + Dunn post-hoc | H=1195.22, p<0.001, all pairs significant |
| ML models | Decision Tree + Random Forest (GridSearchCV) | Best params: max_depth=3, min_samples_leaf=20, n_estimators=200 |
| Evaluation | rRMSE vs naive baseline + Wilcoxon test | RF significant in Clusters 0 & 1 (p<0.05) |
| Interpretability | Permutation importance + PDPs | Thresholds: ~50 heat stress days, ~600 mm precipitation |

---

## Climate Clusters

| Cluster | Label | Countries (n) | Median CV | Wilcoxon vs Naive |
|---|---|---|---|---|
| 0 | Semi-Arid | 9 | 17.8% | p < 0.05 ✓ |
| 1 | Temperate | 24 | 17.4% | p < 0.05 ✓ |
| 2 | Tropical | 5 | 24.8% | n.s. |

> Brazil (BR) and United States (US) are excluded from ML training due to disproportionate cluster representation (98% and 81% respectively), leaving 36 training countries.

---

## How to Run

1. Clone the repository:
```bash
git clone https://github.com/eda-yilmaz/DI501-Term-Project.git
cd DI501-Term-Project
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Download the CY-Bench dataset and place it in the `data/` folder.

4. Run notebooks in order:
```
step3_data_quality → step3_descriptive_stats_table → step4_naive_baseline →
step4b_koppen_models → step5_feature_selection → step5b_clustering →
step6_models → step7_hyperparameter_tuning → step8_statistical_comparison → step8b_comparison → step9_interpretability
```

---

## Key Findings

- Data-driven k-means clustering (k=3) independently confirmed by both elbow method and silhouette analysis (score=0.497), coinciding with the three theory-based Köppen panels.
- The tropical cluster (Cluster 2) exhibits the highest yield instability (median CV=24.8%), consistent with sub-Saharan African rainfall unpredictability.
- The tuned RF reduces rRMSE by 1.4 pp in semi-arid and 0.3 pp in temperate clusters over the naive baseline.
- Partial dependence analysis reveals non-linear thresholds: yield drops sharply beyond ~50 heat stress days and suffers most at 400–600 mm growing-season precipitation.
- Dominant stressor differs by cluster: heat stress drives instability in temperate Europe; precipitation is the binding constraint in semi-arid and tropical systems.

---

## AI Usage Statement

Artificial intelligence was used to assist with code development and language check for drafting parts of the report. All analytical decisions, research questions, and interpretations were made by the author.
