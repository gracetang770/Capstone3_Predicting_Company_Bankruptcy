# Capstone3_Predicting_Company_Bankruptcy

Predicting Company Bankruptcy
Springboard DSC - Capstone 3
Grace Tang
March 2021

## Business Problem:

Predicting company bankruptcy is critical in any financial institution, especially those involved in lending. For such companies, being able to predict whether a business will succeed or fail can result in successful business loans that grow companies, create jobs, and bolster the economy; or result in millions of dollars in losses.

In this project, I developed several binary classification models to predict whether a business is at risk for bankruptcy. The data used is from the Taiwan Economic Journal, ranging from years 1999-2009. The dataset contains approximately 3.2% bankruptcies and 96.8% non-bankruptcies, a highly imbalanced dataset. 

The model with the best recall (fewest false negatives) was Logistic Regression with a recall of 83.33%. 

The model with the best F1-Score (a more balanced precision/recall) was a XGBoost Classifier, with a F1-Score of 0.3465.

## Approach and Techniques Used:

### Exploratory Data Analysis:
* Heatmaps, Histograms, and Boxplots - Found that no feature had an obvious/strong correlation with Bankruptcy.
* Student's T-Test - Found that 56 (60%) features are statistically significant between the two groups (Bankrupt vs. Non-Bankrup), and 38 (40%) features are NOT statistically significant between the two groups.
* Dimensionality Reduction with PCA - The eigenvectors of the first two principal components were investigated; the features which contribute to bankruptcy are:
   * PC 1:
      * ROA (A, B and C) (-)
      * Persistent EPS in the Last Four Seasons (-)
      * Operating Profit Per Share (Yuan ¥) (-)
      * Per Share Net profit before tax (Yuan ¥) (-)
      * Operating profit/Paid-in capital (-)
      * Net profit before tax/Paid-in capital (-)
      * Net Income Total Assets (-)
   * PC 2:
      * Debt ratio % (+)
      * Borrowing dependency (+)
      * Inventory and accounts receivable/Net value (+)
      * Net Worth Turnover Rate (times) (+)
      * Current Liability to Assets (+)
      * Current Liabilities/Equity (+)
      * Current Liability to Equity (+)
      * Liability to Equity (+)
   * Note: (+) indicates an increase in likelihood of bankruptcy, and (-) a decrease in likelihood of bankruptcy.
* Visualizing with t-SNE - The poor separation in t-SNE may indicate that 2 dimensions may be insufficient in representing the internal structure of the data.

### Data Preprocessing and Modeling Approach:
Data was scaled with a log transform, followed by StandardScaler, dimension reduction with PCA, and SMOTE upsampling. Logistic Regression was used as a baseline model. The data preprocessing increased the TPR from 0 to >75%. The data preprocessing steps and model were combined in a pipeline, and each pipeline underwent hyperparameter tuning with Randomized Search 10-fold Cross Validation.

## Results:

|Model|Data Preprocessing|Accuracy|F1-Score|Precision|Recall|ROC AUC|P-R AUC|Runtime (s)|
|:-:|:-:|--:|--:|--:|--:|--:|--:|--:|
|Logistic Regression|No|0.9619|NAN|0.0000|0.0000|0.5887|0.0377|1.0776|
|Logistic Regression|Yes|0.8739|0.2989|0.1821|0.8333|0.9252|0.3020|2.0035|
|Random Forest Classifier|No|0.9707|0.2308|0.7500|0.1364|0.9497|0.4728|1.0542|
|Random Forest Classifier|Yes|0.9355|0.2979|0.2295|0.4242|0.9203|0.2473|6.6547|
|XG Boost Classifier|No|0.9697|0.3404|0.5714|0.2424|0.9472|0.4602|0.3819|
|XG Boost Classifier|Yes|0.9355|0.3465|0.2574|0.5303|0.9086|0.2524|6.2850|

|Model|Data Preprocessing|TP|FN|TN|FP|
|:-:|:-:|--:|--:|--:|--:|
|Logistic Regression|No|0|66|1968|12|
|Logistic Regression|Yes|55|11|1733|247|
|Random Forest Classifier|No|9|57|1977|3|
|Random Forest Classifier|Yes|28|38|1886|94|
|XG Boost Classifier|No|16|50|1968|12|
|XG Boost Classifier|Yes|35|31|1879|101|

* Data Preprocessing involves the following sequential transformations: 
    * Scaling with np.log1p()
    * Scaling with StandardScaler()
    * Dimension reduction with PCA()
    * Appending K-Means Cluster labels as additional features
    * Oversampling the minority class with SMOTE


## Credit:

I would like to thank Chris Esposo for being an awesome Springboard mentor: for teaching me about SMOTE, helping me narrow down ideas, and giving me guidance throughout this project.

I would like to thank Deron Liang and Chih-Fong Tsai (National Central University, Taiwan) for donating this valuable dataset to the UCI Machine Learning Repository, and Federico Soriano Palacios for uploading the dataset to kaggle, where I was able to access it.

## Sources:

Dataset donated by: Deron Liang and Chih-Fong Tsai, deronliang '@' gmail.com; cftsai '@' mgt.ncu.edu.tw, National Central University, Taiwan

Relevant Paper: Liang, D., Lu, C.-C., Tsai, C.-F., and Shih, G.-A. (2016) Financial Ratios and Corporate Governance Indicators in Bankruptcy Prediction: A Comprehensive Study. European Journal of Operational Research, vol. 252, no. 2, pp. 561-572.

Dataset: “Company Bankruptcy Prediction: Bankruptcy data from the Taiwan Economic Journal for the years 1999–2009”: https://www.kaggle.com/fedesoriano/company-bankruptcy-prediction 
