# INCREASING THE SEASONAL FLU VACCINATION RATE

![alt text](data/Flu-Heroes.png)


## Business Understanding

Our client, Flu Heroes, is a vaccine advocacy Non-Governmental Organization that has a goal of improving access to the seasonal flu vaccine to all. The Weekly U.S. Influenza Surveillance Report from the Centers for Disease Control and Prevention (CDC) website detailing outcome of Public Health Laboratories flu tests carried between October, 2021 and February, 2022, reveals a positive rate of c.2% for Influenza A and Influenza B. 

### Goal

The goal of this project is to determine what backgrounds, opinions, or health behaviors predict personal vaccination patterns of individuals. Taking it a step further, Flu Heroes will use insights gleaned from this project in allocating resources to the areas that can increase the annual seasonal flu vaccine numbers. 

## Data Understanding

The data is from the National 2009 H1N1 Flu Survey (NHFS), which was sponsored by the National Center for Immunization and Respiratory Diseases (NCIRD) and conducted jointly by NCIRD and the National Center for Health Statistics (NCHS), Centers for Disease Control and Prevention (CDC). The dataset is from a credible source with over 26,000 observations regarding seasonal flu vaccines, thus it is extremely relevant to our business question. The survey was carried out alongside one regarding the H1N1 swine flu, so we had to extract the data that was utmost concern to our model. The survey was targeted at determining individuals who received the H1N1 vaccine and the seasonal flu shot.

### Data preparation

We used a variety of Python libraries to carry-out this project. 
Pandas  v1.1.3
Numpy   v1.18.5
SciKit-Learn  v0.23.2
Matplotlib v3.3.1

The dataset came as 2 separate files: one containing the target variables and the other had the corresponding features. To start, we merged the two files and started the bigger task of cleaning. 

### Data cleaning
The combined dataframe had  38 columns. 3 of the columns had close to 50% null values. We dropped this columns as inputting the wrong data could cause problems further down the line with our models. We dropped all features directly related to H1N1 flu. Every other null value we filled using modal imputation. Categorical variables were OneHotEncoding. Every feature that went into the model was scaled.



# Final Model: Logistic Regression
We experiment with a total of four models, three of which are logistic regression models and one which is a decision tree model. 

For all of our models, we are using accuracy, precision, and ROC-AUC as our main metrics. Accuracy is an evaluation metric that allows you to measure the total number of predictions a model gets correct, meaning it looks at True Positives and True Negatives. This can give us a general understanding of our model.

We also decided to look closely at precision, because precision considers False Positives in its computation. For our business objectives, False Positives are the surveyees who should have received the vaccine according to our model, but in actuality did not. Minimizing those specific cases is extremely important for our model, since our business objective is to convince the non-vaccinated to get vaccinated through advertisement.

Furthermore, we will use ROC AUC as our final metric, since it tells us how much the model is capable of distinguishing between classes via the False Positive Rate and the True Positive Rate.

### Confusion Matrix
![Confusion Matrix of Final Model]('Phase-3-Project/photos/confusion_finalmodel.png')

True Positives: 6948
True Negatives: 8577
False Positives: 2056
False Negatives 2449

![Violin Plot of Final Model]('Phase-3-Project/photos/violinplot_finalmodel.png')

## Evaluation Metrics
![Confusion Matrix of Final Model]('Phase-3-Project/photos/evalmetrics_finalmodel.png')

Mean accuracy of the final model: 0.773489765351972

Precision Score of the final model: 0.7716570413149711

AUC of the ROC Curve of the final model: 0.85

![ROC-AUC of Final Model]('Phase-3-Project/photos/ROCAUC_finalmodel.png')

## Feature Importance
What are the most important features for predicting whether one would receive the seasonal vaccine? We aim to find out using the `ExtraTreesClassifier` method. This class implements a meta estimator that fits a number of randomized decision trees (a.k.a. extra-trees) on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting.

![Top 10 Feature Importance]('Phase-3-Project/photos/top10feature.png')

`doctor_recc_seasonal` - Seasonal flu vaccine was recommended by doctor. (binary)

`opinion_seas_vacc_effective` - Respondent's opinion about seasonal flu vaccine effectiveness

`opinion_seas_risk` - Respondent's opinion about risk of getting sick with seasonal flu without vaccine.

It turns out that the `doctor_recc_seasonal`, `opinion_seas_vacc_effective`, and `opinion_seas_risk` are the top three most important features in determining whether someone received the seasonal vaccine. From this analysis, we recommend that Flu Hereos specifically tailor their advertisement and campaign efforts to emphasizes the aforementioned features. 


# Conclusion

We recommend that our stakeholder Flu Heroes tailor their advertisements to emphasize the fact there is a high risk of getting sick without the vaccine and that the seasonal flu vaccine has high effectiveness. Furthrmore, their campaign tactics should highlight that the seasonal flu vaccines were recommended by doctors. Since our final logistic regression model yields the highest accuracy, precision, and AUC scores, it can be used to predict whether or not a person would receive the seasonal flu vaccine based on his or her background information, opinions, and health behaviors. For further implementations, we could not only pinpoint which specific audience to target with advertisements, but also apply knowledge from other pandemics such as Covid-19, SARS, and H1N1. These new findings may augment our models, giving us the ability to better understand important features and predict vaccination rates.