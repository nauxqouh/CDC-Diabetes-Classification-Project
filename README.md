# 👨‍⚕️🏥 CDC Diabetes Health Indicator

This repository contains demonstrating code for the report of the project `CDC Diabetes Health Indicator` in Statistical Processing for Data Science coursework.

Members for this group project:
1. Ba Truong Binh
2. Giao Chiem Huynh
3. Han Nguyen Ngoc Bao
4. Huong Nguyen Thi Xuan
5. Linh Phan Thi Ngoc
6. Thu Ho Tran Anh

## About Data
The Behavioral Risk Factor Surveillance System (BRFSS) is a health-related telephone survey that is collected annually by the CDC. Each year, the survey collects responses from over 400,000 Americans on health-related risk behaviors, chronic health conditions, and the use of preventative services. It has been conducted every year since 1984. For this project, a csv of the dataset available on Kaggle for the year 2015 was used. This original dataset contains responses from 441,455 individuals and has 330 features. These features are either questions directly asked of participants, or calculated variables based on individual participant responses.

This dataset contains 3 files:

- `diabetes _ 012 _ health _ indicators _ BRFSS2015.csv` is a clean dataset of 253,680 survey responses to the CDC's BRFSS2015. The target variable Diabetes_012 has 3 classes. 0 is for no diabetes or only during pregnancy, 1 is for prediabetes, and 2 is for diabetes. There is class imbalance in this dataset. This dataset has 21 feature variables
- `diabetes _ binary _ 5050split _ health _ indicators _ BRFSS2015.csv` is a clean dataset of 70,692 survey responses to the CDC's BRFSS2015. It has an equal 50-50 split of respondents with no diabetes and with either prediabetes or diabetes. The target variable Diabetes_binary has 2 classes. 0 is for no diabetes, and 1 is for prediabetes or diabetes. This dataset has 21 feature variables and is balanced.
- `diabetes _ binary _ health _ indicators _ BRFSS2015.csv` is a clean dataset of 253,680 survey responses to the CDC's BRFSS2015. The target variable Diabetes_binary has 2 classes. 0 is for no diabetes, and 1 is for prediabetes or diabetes. This dataset has 21 feature variables and is not balanced.

Follow link for more information: https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset

Variable lookup list at https://www.cdc.gov/brfss/annual_data/2015/pdf/codebook15_llcp.pdf

_Here, we used the `diabetes _ 012 _ health _ indicators _ BRFSS2015.csv` dataset._

## Handling Imbalanced Data Result based on Multinominal Logistic Regression

<img width="910" alt="Screen Shot 2025-03-07 at 15 29 27" src="https://github.com/user-attachments/assets/1525227e-9a70-4de0-8715-c73c4425c4f3" />

| Methods                         | Accuracy  | Kappa     | Macro-F1  |
|----------------------------------|----------|----------|----------|
| Under Sampling                  | 0.5032397 | 0.2548596 | 0.1245795 |
| Over Sampling                   | 0.5143988 | 0.2715983 | 0.1327445 |
| SMOTE                            | 0.5179986 | 0.2769978 | 0.1367898 |
| Class weight                     | 0.5154788 | 0.2732181 | 0.1337437 |
| Under Sampling + SMOTE           | 0.5147588 | 0.2721382 | 0.1343537 |
| Under Sampling + Over Sampling   | 0.5158387 | 0.2737581 | 0.1339996 |

The method that our team select is **Combined Data** (Undersampling + SMOTE).


## Multi-Classification with top 10 features Result

```
top_features
```
```
##  [1] "gen_hlth"               "high_bp"                "bmi"                   
##  [4] "diff_walk"              "high_chol"              "age"                   
##  [7] "heart_diseaseor_attack" "phys_hlth"              "income"                
## [10] "education
```

| Model                         | Accuracy  | Kappa     | Macro-F1  |
|---------------------------------|----------|----------|----------|
| Multinomial Logistic Regression | 0.5147588 | 0.2721382 | 0.1343537 |
| **Random Forest**                   | **0.7739381** | **0.6609071** | **0.4669010** |
| Naive Bayes                     | 0.5007199 | 0.2510799 | 0.1217087 |

The model that best explains is Random Forest with Combined Data.

```
## $Precision
## Non-diabete Pre-diabete     Diabete 
##   0.7407407   0.8439024   0.7482725 
## 
## $Recall
## Non-diabete Pre-diabete     Diabete 
##   0.7559395   0.7473002   0.8185745 
## 
## $Accuracy
## [1] 0.7739381
## 
## $Kappa
## [1] 0.6609071
## 
## $Macro_F1
## [1] 0.466901
```


## Multi-Classification with only Health Indicators Result

health_indicators

```
gen_hlth + high_bp + bmi + diff_walk + high_chol + heart_diseaseor_attack + phys_hlth
```

| Model                         | Accuracy  | Kappa     | Macro-F1  |
|---------------------------------|----------|----------|----------|
| Multinomial Logistic Regression | 0.5057595 | 0.2586393 | 0.1252183 |
| **Random Forest**                   | **0.7760979** | **0.6641469** | **0.4704440** |


## Binary-Classification for Non-diabete or Diabete Result

| Model                         | AUC  | ROC Curve     |
|---------------------------------|----------|----------|
| Logistic Regression | 0.8113 | <img width="693" alt="Screen Shot 2025-03-07 at 15 48 52" src="https://github.com/user-attachments/assets/ae8dbbf4-74da-4024-afa7-7c486d133ccd" /> |
| Random Forest       | 0.7969 | <img width="694" alt="Screen Shot 2025-03-07 at 15 49 05" src="https://github.com/user-attachments/assets/6847d68d-57f4-45cc-89c2-d1dd7fca287b" /> |
| Naive Bayes         | 0.7947 | <img width="688" alt="Screen Shot 2025-03-07 at 15 49 51" src="https://github.com/user-attachments/assets/c38eb1f3-7c6b-4aae-8e86-6ed2dcb1c415" /> |

The Logistic Regression model has an AUC index of 0.81, which shows that the model's ability to distinguish between classes is quite good and reliable.

