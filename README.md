# Heart Failure Mortality Prediction (R)

Can routine clinical measurements predict which heart failure patients will die during follow-up? This project runs a full data mining pipeline in R on 299 patient records: exploration, cleaning, preprocessing, clustering, and classification.

## Results

| Model | Cross-validated accuracy | Test accuracy |
|---|---|---|
| **Decision tree** | 82.0% | **75.0%** |
| kNN (k = 7) | 77.7% | 69.3% |

The decision tree was the stronger model, with **AUC 0.838**, **recall 0.821**, and precision 0.575 on the held-out test set. It caught 82% of actual deaths, which matters most in a medical setting, where missing a real death is worse than a false alarm.

**Other findings:**
- Patients who died had **higher serum creatinine** and **lower ejection fraction** on average, making these the clearest warning signs in the data.
- K-means clustering (k = 2) partly separated survivors from deaths. One cluster was 62% deaths and the other was 86% survivors, but the clusters overlapped a lot.

## Methods

1. **Exploration:** histograms, boxplots, bar charts, correlation matrix, and scatterplots
2. **Cleaning:** checked for missing values (none) and outliers (kept, since they're clinically plausible), and converted binary variables to factors
3. **Preprocessing:** centered and scaled the 7 numeric variables for kNN
4. **Clustering:** K-means with elbow and silhouette methods, visualized with PCA
5. **Classification:** 70/30 train/test split, with 10-fold cross-validation to tune a decision tree (`rpart`) and kNN
6. **Evaluation:** confusion matrix, precision, recall, ROC curve, and AUC

## Limitations

- **Small dataset:** with only 299 patients, the test set is about 90 patients, so results can shift a lot with a different split.
- **The `time` variable:** it's the length of follow-up, and patients who died early naturally have short follow-up times. That makes it partly a proxy for the outcome, so a stricter version of this model would drop it.

## Data

[Heart Failure Clinical Records](https://www.kaggle.com/datasets/andrewmvd/heart-failure-clinical-data) (Kaggle), originally from Chicco & Jurman (2020), *BMC Medical Informatics and Decision Making*.

## Run It

Open `heart_failure_analysis.Rmd` in RStudio with the CSV in the same folder, then click **Knit**.

Required packages: `tidyverse`, `caret`, `GGally`, `factoextra`, `pROC`, `rpart`

## Files

| File | Description |
|---|---|
| `heart_failure_analysis.Rmd` | Full analysis in R Markdown |
| `heart_failure_clinical_records_dataset.csv` | Dataset (299 patients, 13 variables) |
