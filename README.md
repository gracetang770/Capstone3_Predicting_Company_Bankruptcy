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


## Data: 
“Company Bankruptcy Prediction: Bankruptcy data from the Taiwan Economic Journal for the years 1999–2009”: https://www.kaggle.com/fedesoriano/company-bankruptcy-prediction 

## 
## 
