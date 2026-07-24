# From Prediction to Policy: Smoking Cessation Prediction with Machine Learning

Predicting successful smoking cessation using six years of BRFSS survey data (2018-2023), with identification of high-risk groups and stable predictors for policy design.

**Authors:** Armin Khojavi, Hamed Hesami, Mahdieh Ebrahimi

---

## Abstract

This project models successful smoking cessation using six years of BRFSS data (CDC's Behavioral Risk Factor Surveillance System) and machine learning models (Logistic Regression, LightGBM, XGBoost, CatBoost), combined with comprehensive modeling approaches (Data Pooling, Temporal Ensemble, Stacking). Feature effects and their temporal stability were assessed via SHAP.

**Best model:** Stacking Ensemble (LightGBM + XGBoost → Logistic Regression meta-model)
`AUC: 0.7881` `Accuracy: 0.7446` `F1: 0.7330`

---

## Data

- Source: BRFSS (CDC), 2018-2023, repeated cross-sectional longitudinal design
- Sample: respondents with a lifetime history of smoking at least 100 cigarettes (`smoke100=1`)
- Target: binary — successful cessation (`_SMOKER3`, former smoker) vs. current smoker
- Leakage-prone features (`smoke100`, `_rfsmok3`) were removed from predictors.

---

## Methodology

- **Preprocessing:** standard pipeline (imputation/encoding/scaling), survey weights `LLCPWT`, class imbalance handled via `scale_pos_weight`
- **Feature selection:** All Features vs. VIF-selected (VIF < 7); methods included SelectKBest, RandomForest Importance, RFE
- **Models:** classic (Logistic Regression, Decision Tree, LDA, LR+PCA) and boosting (LightGBM, XGBoost, CatBoost)
- **Comprehensive modeling:** Temporal Ensemble, Data Pooling, Stacking Ensemble (`cv=5`)
- **Interpretability:** coefficients/odds ratios for linear models, SHAP for boosting models

---

## Key Findings

- LightGBM and CatBoost consistently achieved the best performance (AUC 0.77-0.79); All Features outperformed VIF-selected.
- Predictive patterns remained stable even through the COVID-19 pandemic.
- **Increases cessation odds:** older age (strongest predictor, OR: 1.47-2.67), being married, higher income/education, higher BMI and weight, serious disease diagnosis (COPD, stroke, depression), regular physical activity and checkups
- **Decreases cessation odds:** poorer general health, poor mental health (effect intensifying from 2019/2020 onward)
- Common limitation: all models were biased toward the majority class (successful cessation).

---

## Strengths and Limitations

**Strengths:** large national dataset, 6-year coverage, SHAP interpretability, comprehensive modeling
**Limitations:** self-reported data (recall/social desirability bias), simplified definition of "successful cessation," class imbalance, limited variable granularity

---

## Future Directions

True longitudinal data · multi-faceted interventions · class imbalance techniques (SMOTEBoost) · deeper geographic analysis (county-level) · deeper meta-model analysis in Stacking

---

## References

1. Zhu et al. (2025), JNCI — [Link](https://academic.oup.com/jnci/advance-article/doi/10.1093/jnci/djaf121/8164449)
2. Sharbaugh et al. (2018), PLOS ONE — [Link](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0204416)
3. Mills et al. (2021) — [Link](https://pmc.ncbi.nlm.nih.gov/articles/PMC8139454/)
4. Berkowitz et al. (2016), Cancer Epidemiology, Biomarkers & Prevention — [Link](https://aacrjournals.org/cebp/article/25/10/1402/70704/)
5. Parikh et al. (2022), Stroke — [Link](https://www.ahajournals.org/doi/full/10.1161/STROKEAHA.121.036941)
6. Kasteridis & Yen (2012) — [Link](https://pmc.ncbi.nlm.nih.gov/articles/PMC3401400/)
7. Bandi et al. (2022), JAMA Network Open — [Link](https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2794810)

---

`Smoking Cessation` `Machine Learning` `BRFSS` `SHAP` `Ensemble Stacking` `LightGBM` `XGBoost` `CatBoost`
