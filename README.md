CHD-MIST: Clinical Data Integrity Stress Testing for Coronary Heart Disease Prediction

CHD-MIST is a stress-testing framework that checks whether the machine-learning model that looks best on clean clinical data is also the most reliable when data integrity is degraded. It applies controlled measurement noise, missing values and label noise to a coronary heart disease (CHD) dataset and compares six classifiers on how well they retain their clean-data performance.
 
Key idea

Clean-data accuracy is the usual criterion for choosing a clinical prediction model, but real clinical data contain measurement error, missing observations and incorrect labels. CHD-MIST adds a robustness-based evaluation layer on top of clean-data evaluation and compares the two model rankings.

Framework overview

1. Data preparation: stratified 80:20 train/test split, `StandardScaler` for LR, SVM and KNN.
2. Baseline models: six classifiers trained on clean data.
3. Controlled stress generation: four stress types, five severities (0%, 5%, 10%, 15%, 20%), 20 repetitions each.
4. Robustness measurement: integrity score, mean AUC degradation, worst-case integrity, bootstrap 95% CIs.
5. Statistical comparison: pairwise Wilcoxon signed-rank tests with FDR (Benjamini–Hochberg) correction, plus rank-biserial effect sizes.
6. Ranking comparison: clean-data ranking vs. robustness-based ranking.

Models

Logistic Regression (LR), Decision Tree (DT), Random Forest (RF), Support Vector Machine (SVM, RBF), K-Nearest Neighbors (KNN, k = 5) and XGBoost. All use fixed settings without hyper-parameter tuning (see the paper, Section III-C).

Datasets

Cardiovascular Disease Dataset [Mendeley Data](https://doi.org/10.17632/dzz48mvjht.1) (Doppala & Bhattacharyya, 2021) 1,000 (12 predictors) Primary
Cleveland Heart Disease  [UCI ML Repository](https://doi.org/10.24432/C52P4X) (Janosi et al., 1989) 303 External check 

Both datasets are public. Please download them from the original sources and follow their licences.


Findings

- XGBoost has the best clean-data ROC-AUC, but Random Forest is the most robust (highest mean and worst-case integrity), so clean-data performance and robustness can lead to different model choices.
- Label noise is the most damaging stress (mean integrity 97.40); measurement perturbation is the mildest (99.87).
- Decision Tree is the most sensitive model.
- On the primary dataset, these findings were stable across five additional train/test splits.
- On the small external Cleveland dataset (303 patients), only the label-noise result was reproduced; model rankings were unstable across splits, so it should not be read as validation of the rankings.

