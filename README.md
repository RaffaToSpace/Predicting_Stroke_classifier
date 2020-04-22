# Predicting_Stroke
In this project I have developed a simple predictor for stroke in healthcare patients, based on real-world data. The idea is to develop a few ideas on how to deal with medical data and possible unbalances, biases and distortions due to the way the data has been collected and structured. In the first version of the project I due some quick data exploration and cleaning/feature engineering, with the aim of quickly producing a predictor. Further work could be done on the feature selection, on modularisation, code cleaning and ultimately on the predicting model optimisation.
## Contents of this project:
- **Data description**;
- **Data exploration**;
- **Data cleaning and feature eng.**;
- **Model construction and optimisation**;
- **Conclusions and final report**

## Data description
Each patient is characterised by the following variables:

<img src="https://github.com/RaffaToSpace/Predicting_Stroke/blob/master/images/data_desc.png" alt="drawing" width="500"/>

## Data exploration
In this section I check the variables's distribution and balancing. Some imbalances withing features are found, e.g. on heart disease and hypertension occurrence, but it would not be realistic to expect a balanced distribution in a random population sample. Other generic descriptive variables such as age, body-mass index and glucose level follow a normal distribution, as shown in the attached plots.

<img src="https://github.com/RaffaToSpace/Predicting_Stroke/blob/master/images/all_hist.png" alt="drawing" width="1000"/>

The target variable _stroke_ is however very unbalanced, with only 1.8% of the sample with value equal to 1, and that would likely cause the predictor to ignore the minority class.

## Data cleaning and feature eng.
#### Missing values
Values are missing in two columns, _bmi_ and _smoking_status_. As regards _bmi_, the missign values are 3.4% of the total, and I decided to fill them with the average value.  
Regarding _smoking_status_, I decided to fill them with "_never smoked_" value, and to create a variable _missing_smoking_status_, with values (0,1), equal to 1 if the _smoking_status_ information was missing.
#### Encoding non-numerical values
For all non-numerical categorical values, I used the LabelEncoder() function to convert them into numerical values.
#### Balancing the data through over-sampling
I opted to rebalance the target variable _Stroke_ through over-sampling, by using the Synthetic Minority Oversampling Technique (SMOTE), which generates synthetic data. In the resampled dataset, the “stroke” target variable is equally distributed with 29470 samples per value.

## Model construction and optimisation
As a predictive model, I chose a random forest classifier, as it handles categorical variables well and it is more resistant to overfitting than single decision trees. For a more complete description on the optimisation process and model performance, please refer to the attached report.  
the model performs well with a F1 score of 0.93 and a value of area under the ROC curve of 0.98.

<img src="https://github.com/RaffaToSpace/Predicting_Stroke/blob/master/images/scores_ROC.png" alt="drawing" width="1000"/>

The relative importance of features in shown in the attached table. We can see how _Age_, _avg_glucose_level_, _bmi_, _ever_married_, _work_type_ make up roughly 85% of the relative importance. It should be noted that _smoking_status_ is not amongst the most important features, and actually the fact that the information is missing is more important than the value itself.

<img src="https://github.com/RaffaToSpace/Predicting_Stroke/blob/master/images/feat_imp_table.PNG" width="300"/>

## Conclusions and final report
I have built a simple random forest classifier for the provided dataset which reliably classifies patients that suffered a stroke. I preprocessed the data and optimised the model parameters in order to maximise performance, and the final model has a probability of 98% of distinguishing between the classes. The analysis allowed me to identify a subset of features that impact the most on the model, which means that an accurate model may be built with a lower number of features, 5 instead of 10 in this case. 
Such a model could be used to identify patients with potential risks of suffering a stroke, or to study potential correlations between occurrence of stroke and other health or lifestyle factors.


I have written a short report that provides some explanation on the work done, and a discussion on the choices made when handling the data and choosing the model. Note that numbers might differ slightly to ones in the notebook, as small changes to the model have been done. 
