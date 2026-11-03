# Explainable Automated Valuation Model (AVM) Based on Leakage-Resistant Spatial Feature Engineering

Code, configuration, and result tables for the manuscript submitted to the *International Journal of Advances in Data and Information Systems (IJADIS)*.

## Summary

This study develops an explainable AVM for U.S. property prices using XGBoost, SHAP, and hierarchical spatial features (ZIP, ZIP3, state, and city price per square foot) estimated out-of-fold to avoid target leakage. Five models (Random Forest, LightGBM, CatBoost, XGBoost, and a Stacking Ensemble) are tuned with the same Optuna budget and compared on a random test split and under ZIP-grouped validation. An ablation study, a negative control (shuffled targets), and SHAP analysis support the results.

## Data

- **Source:** USA Real Estate Dataset on Kaggle (Realtor.com listings): `[https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset]`
- **License / usage terms:** see the Kaggle dataset page `[insert license]`
- **The raw data are NOT included in this repository.** Download them from Kaggle and place the CSV in the `data/` folder (see `data/README.md`).
- The target is `price`, which is the current listing price or, for recently sold properties, the latest sale price.

## Key settings

| Item | Value |
| --- | --- |
| Random seed | 42 |
| Sample size | 400,000 records (price-decile stratified sample) |
| Records after cleaning | 295,195 |
| Train / test split | 80/20 random (236,156 / 59,039) |
| Price filter | 10,000 to 5,000,000 USD |
| house_size filter | 200 to 15,000 sq ft |
| Optuna | TPE sampler, 30 trials per model, 3-fold CV on a 25% training subsample |
| Geographic validation | 5-fold GroupKFold by ZIP code |
| Python | 3.13.16 |

The full configuration is in `outputs/environment_config.json`.

## How to run

1. Clone the repository.
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Download the dataset from Kaggle and place the CSV in `data/`.
4. Open `notebooks/Prediksi_Harga_Property_REVISI_4.ipynb`, set the data path at the top of the notebook, and run all cells from top to bottom.
5. Results are written to the `outputs/` folder.

Note: Optuna tuning took about 181 minutes and the Stacking fit about 15.6 minutes in the original run. Set `DEBUG = True` in the configuration cell for a quick test run.

## Contents of `outputs/`

| File | Used for |
| --- | --- |
| `table_main_random_test.csv` | Table 2: model comparison on the test set |
| `table_ablation.csv` | Table 3: ablation of engineered features |
| `train_test_gap.csv`, `table_reporting_cv.csv` | Table 4: training/test gap and cross-validation |
| `table_geo_cv_summary.csv`, `table_geo_cv_folds.csv` | Table 5: ZIP-grouped geographic validation |
| `predictions_test.csv` | Table 6 (price deciles) and Figure 3; test-set predictions of all models |
| `table_metrics_by_status.csv`, `table_metrics_property_overlap.csv` | Table 7: accuracy by listing status and train-test overlap |
| `table_paired_comparison.csv` | Table 8: paired comparison of XGBoost with other models |
| `table_shap_importance.csv` | Table 9: mean absolute SHAP values |
| `shap_beeswarm.png`, `shap_bar.png` | Figures 4 and 5 |
| `actual_vs_predicted.png`, `residuals.png` | Figure 3 |
| `table_cleaning_steps.csv` | Data cleaning steps |
| `table_best_hyperparameters.csv`, `best_params.json` | Selected hyperparameters |
| `optuna_trials_*.csv` | Optuna trial history per model |
| `negative_control.csv` | Negative control (shuffled targets) |
| `run_summary.json`, `environment_config.json` | Run summary and software configuration |

Some column labels in the CSV files are in Indonesian or use internal version names (for example, "REVISI_3", "REVISI_4", "Pembanding" = comparator, "Langkah" = step, "Dibuang" = removed). They do not affect the results.

## Citation

If you use this code, please cite the manuscript and the archived repository:

```
N. A. Fadillah, R. Dhenabayu, A. Kautsar, Z. H. Aminah, and A. R. Shaikh,
"Explainable Automated Valuation Model (AVM) Based on Leakage-Resistant
Spatial Feature Engineering," Int. J. Adv. Data Inf. Syst., [year].
Code: https://github.com/[username]/property-avm-xgboost, DOI: [Zenodo DOI]
```

## License

Code is released under the MIT License (see `LICENSE`). The dataset is not covered by this license and remains subject to its original terms.
