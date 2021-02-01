# COVID-19: Symptoms and Predictions

#### By David Cortes, Nao Kawakami, Peter Yonka, Ryan Scribner

## Problem Statement

Utilizing the Coronavirus Disease 2019 (COVID-19) Clinical Data Repository, we will examine the influence of individual symptoms on whether a COVID test will be positive. We hope that the understanding gained will help frontline medical works with limited time and resources to triage cases and determine initial steps in creating treatment plans.

## Data

The COVID 19 symptom data used in this project was obtained from Carbon Health, a clinic in California. The data is maintained as CSV files and is compliant with HIPAA Privacy Rule's De-Identification Standard. It includes clinical characteristics such as epidemiologic factors, comorbidities, vitals, clinician-assessed symptoms, and patient-reported symptoms, as well as radiological and laboratory findings.

The data also has positive and negative test results for both symptomatic and asymptomatic patients. It does not include results for patients with severe symptoms, as those patients are referred to ER.

Details about each feature are available in the [data dictionary](https://docs.google.com/spreadsheets/d/1p9rtv2LjVCPb54MdGe8ZqJ1zF3McIFnzq-ZhhjWgguI/edit?usp=sharing).

## Modeling

Two datasets were designed and analyzed with two different purposes:
1. Identifying the most important symptoms to accurately assess patients for COVID 19.
2. Accurately predicting whether or not a patient will test positive based on their symptoms.

#### Model 1

Since the interpretability of feature influence is essential for this model, the symptoms in the data were split into two groups:
- Patient reported features
- Patient reported features combined with clinically collected/assessed features

Each dataset was run through a logistic regression optimizing for true positives and analyzed at the 99% confidence level (alpha = 0.01).

RandomOverSampler, RandomUnderSampler, and imbalanced-learn Pipeline were used for model 1. The Grid Search Logistic Regression Model Scores are shown below:
- Training accuracy score: 0.868
- Testing accuracy score: 0.868
- Training recall score: 0.526
- Testing recall score: 0.537

The combined patient and clinical results were then interpreted. Three of these interpreted features are shown below:
- A patient is 1.383 times as likely to test positive for COVID-19 for every 1-unit increase in the onset measurement, all else held constant.
- A patient is 1.313 times as likely to test positive for COVID-19 for every 1-unit increase in cough rating, all else held constant.
- A patient is 1.114 times as likely to test positive for COVID-19 for every additional breath per minute in respiratory rate, all else held constant.

#### Model 2

The dataset for model 2 was cleaned and modeled using classification models and a voting classifier to maximize predictive power.

This model helps frontline medical workers pre-screen and prioritize potential patients, and it also aids in grouping them based on the results in order to avoid further infection onsite.

AdaBoostClassifier, GradientBoostingClassifier, DecisionTreeClassifier, KNeighborsClassifier, and XGBClassifier were tested for model 2. The best scores are shown below:
- Training accuracy score: 0.97
- Testing accuracy score: 0.93

## Findings and Conclusion

#### Model 1
The imbalanced classes were offset by utilizing over/undersampling techniques only to a point. However, the fit models do provide insight into the influence of symptoms in relation to a patient testing positive for COVID-19.

#### Model 2
The predictive models are very accurate, although they aren't accurate enough for use in the medical field. An accuracy of 99% is preferable for the medical field.

## Next Steps

#### Model 1
- Gather more data
    - Potentially pool data with other clinics
    - Gain access to more positive test results
- Test alternative over/undersampling methods
- Communicate with Carbon Health in order to gain some clarity on clincally collected data
- Dashboard with symptom metrics updated with new data as it is available

#### Model 2
- Tune hyperparameters
- Add more classifiers
- Add more positive test sample
    - Since the vast majority of test results are negative, adding more positive results would help make the data less imbalanced

## Works Cited

- https://covidclinicaldata.org/
- https://carbonhealth.com/coronavirus
- https://github.com/mdcollab/covidclinicaldata
- https://docs.google.com/spreadsheets/d/1p9rtv2LjVCPb54MdGe8ZqJ1zF3McIFnzq-ZhhjWgguI/edit?usp=sharing
