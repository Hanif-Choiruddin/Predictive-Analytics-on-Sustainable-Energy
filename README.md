# Predictive Analytics on Sustainable Energy
Preliminary Round DAC PRS 2024

# TEAM
1. Hanif Choiruddin, Statistika ITS
2. Daniswara Aditya Putra, Statistika ITS

# Introduction
Recent decades have seen tremendous changes in the global energy industry,
with solar energy emerging as a key element in the search for sustainable energy
solutions. Solar energy has emerged as a crucial component in lowering
dependency on fossil fuels and guaranteeing that everyone has access to clean,
reasonably priced, and dependable energy as nations around the world work to
meet climate targets. In order to accomplish these goals, solar power systems'
dependability and efficiency are essential since they have a direct effect on the
total output and sustainable energy production.
Leader in the solar energy industry DAC Green Energy Company encounters
difficulties in maximising solar power production, especially in improving energy
output forecasts. For the purpose of increasing operating efficiency, lowering
uncertainty, and advancing sustainable energy goals, accurate solar energy
generation forecasting is crucial. DAC Green Energy wants to reduce production
losses, improve operational planning, and make the energy grid more dependable
by making improvements to prediction models.
In order to optimize the generation of solar energy, this research examines the
environmental and meteorological factors that impact solar output. The data
gathered in the 2014-2017, which includes information on sun irradiance, cloud
cover, temperature, wind speed, and humidity—is the main subject of this study.
Developing solutions to increase energy production efficiency, decrease
inefficiencies, and improve total energy output sustainability is the aim of this
investigation.
Based on the energy storage capacity, this study uses machine learning
techniques, specifically the CatBoost model, to forecast the percentage of baseline
energy generated in an hour. This analysis aims to offer greater insights into how
environmental and meteorological elements affect solar energy output and assist
DAC Green Energy in enhancing its solar panel technology and operational
methods. It does this by utilizing data from various sources.

# ANALYTICAL STEP
![PPP drawio](https://github.com/user-attachments/assets/aa8d30f0-e6db-4d36-9f1f-379a3cb96598)

## PRA-PREPOCESSING DATA
In this analysis there are 2 types of data, namely wheater data and solar
data, both data are divided into train and test. Train data and test data have the
same variables, but the test data does not have a response variable, namely
'Baseline', to facilitate analysis, the two data are combined based on 'Year',
'Month', 'Date', and 'Time'.So that the results given are valid, we divide the data on
the train data, so there are 3 pieces of data, namely train data, validation data, and
test data

## PREPOCESSING DATA
The data we use has a missing value, data that has an object type and has a
missing value will be replaced by the mode of the data, then data that has a float
type will be replaced by the mean of the data. then we create 1 more column as an
index called 'Datetime' which has 'YYYY%MM%DD%TT% as an index.

## FEATURE SELECTION
Feature selection is an important process in machine learning that aims to
select the most relevant and informative subset of features for a prediction model.
In research and practice, proper feature selection can improve model performance,
reduce overfitting, and speed up the model training process. In this section, the
RandomForestRegressor model is trained using the 'y_train' and 'x_train' training
data. After training, variable selection from the model is used to obtain the
importance of each feature. This value is then combined with the feature name in
the form of a DataFrame for easy analysis.Features are sorted by importance, and
a threshold is set to separate “good” (important) features from “bad” ones.
Features with importance values below the threshold are considered less relevant
and are not selected for use in the model.

## MACHINE LEARNING MODELING
CatBoostRegressor is a boosting-based machine learning algorithm
developed by Yandex. It is a highly efficient gradient boosting algorithm that
works well on tabular data, especially when there are categorical features that
require good coding.Using CatBoostRegressor and preset parameters, you build a
model optimized to predict the target value. The MSE, MAE, and R² metrics
provide insight into the model's performance, with a focus on accuracy and the
model's ability to capture data variability

# DISCUSSION AND RESULT
## ABOUT DATA
### MISSING VALUE
![image](https://github.com/user-attachments/assets/f7c2fbc5-8e80-45ce-ba18-08be428228bc)
In this study, handling missing values is a crucial step in ensuring the
integrity and reliability of the predictive model. The dataset contains both
categorical and numerical variables, and different strategies are employed to
address missing values for each type.
For the categorical variable "weather_type", missing values are imputed
using the mode of the feature. The mode represents the most frequently occurring
value in the dataset, which is a common approach for handling missing
categorical data. This method helps preserve the overall distribution and
characteristics of the data.
For the numerical variable "humidity", missing values are imputed with
the mean of the feature. The mean provides a measure of central tendency and is
used to fill in missing values in a way that maintains the overall statistical
properties of the data. This approach is widely used in practice and helps ensure
that the imputation does not introduce significant bias into the dataset.
By applying these imputation techniques, the dataset is prepared for
further analysis and modeling, ensuring that missing values do not adversely
affect the performance of the predictive models.
### ENCODING DATA
![image](https://github.com/user-attachments/assets/a9c05f0d-dd5d-499e-8690-0d5067468a13)

To facilitate machine learning modeling, it is essential to convert
categorical variables into a format that algorithms can interpret. This process is
known as encoding. In this study, we use Label Encoding to achieve this
transformation.
The LabelEncoder from the sklearn.preprocessing library is utilized for
encoding. This encoder transforms each categorical value into a corresponding
integer label, ensuring that the data is in a format suitable for model training.
In this study, we employ Label Encoding to transform categorical variables
into numerical values. The following variables are encoded using LabelEncoder:
### RESPONSE DATA (%BASELINE)
The baseline variable, representing the "Percentage of energy generated in
one hour based on the energy storage capacity," exhibits a skewed distribution
with a wide range of values. The minimum value is 0, indicating that in some
cases, no energy was generated within an hour, while the maximum value of
10.169 suggests that in certain instances, energy generation significantly exceeded
the storage capacity.
![image](https://github.com/user-attachments/assets/a4277471-ca97-4ee5-ac36-1eac629dc8bc)

In the exploratory data analysis (EDA) phase, we visualized the
distribution of the 'baseline' variable. The distribution plot shows that the majority
of baseline values cluster around a very low range, close to 0. This indicates that
the initial conditions (baseline) of most data tend to be at a low level.
However, there is a small amount of data with significantly higher baseline
values. The presence of these extreme values should be further investigated. It is
possible that these extreme values represent unique or different conditions from
the majority of the data.
The positively skewed distribution shape indicates that the distribution of
baseline data is not symmetrical. The long right tail of the distribution shows the
presence of some observations with baseline values that are much higher than the
average.

### FEATURE SELECTION
This section describes the feature selection process employed to identify
the most relevant features for predicting the baseline variable, which represents
the "Percentage of energy generated in one hour based on the energy storage
capacity."
We utilized a Random Forest Regressor model to assess the importance of
each feature in predicting the baseline. The model's feature importances provide
insights into the contribution of each feature to the model's prediction accuracy.
The analysis revealed fourteen features with the highest importance scores.

### MODELING AND PREDICTION
In this section, we describe the development and evaluation of a machine learning
model to predict Baseline (%). We employed a CatBoostRegressor model with the
following hyperparameters:
![image](https://github.com/user-attachments/assets/9853ea95-8226-4913-8dc9-f7329b79aa17)

The model was trained on the training data (X_train, y_train) and
evaluated using a stratified validation split. This approach ensures that the model's
performance is assessed on unseen data and helps prevent overfitting.
The model achieved promising results on the validation set,**with a Mean
Squared Error (MSE) of 0.0096, a Mean Absolute Error (MAE) of 0.0644, and an
R-squared score of 0.8591.** These metrics indicate that the model can accurately
predict the target variable on unseen data within the validation set.
However, when the model was applied to predict on a new unseen dataset
(prediction file), the accuracy score obtained is 0.0047. This discrepancy
highlights the limitations of machine learning models. While the model performed
well on the data it was trained on, it may not generalize well to entirely different
data distributions.

# CONCLUSION
The analysis using the CatBoostRegressor model for forecasting the
percentage of baseline energy generated in an hour by DAC Green Energy
Company has yielded insightful results. The model demonstrates a robust
predictive capability with a high validation R-squared score of 0.8591, reflecting
its accuracy on the training data and and the accuracy of the score obtained from
the test data prediction is 0.0047. Key environmental and meteorological factors
influencing solar energy generation include time of day, humidity, solar zenith
angle, surface albedo, and cloud coverage. However, discrepancies in model
performance on unseen data suggest that the model is sensitive to shifts in data
distribution, as evidenced by the significant drop in the R-squared score when
applied to new datasets.
The analysis identified that reflective surfaces (surface albedo) positively
influence energy generation, while factors like solar zenith angle and sunset are
inversely correlated with energy output. Moreover, the baseline distribution
exhibits significant skewness, with most energy generation events clustered
around low values, suggesting variability in energy efficiency across different
conditions. and recommendation.
1. Improving Generalization: To address the decline in model performance
on unseen data, future iterations should focus on model generalization
techniques such as cross-validation on a wider range of datasets, or
introducing domain-specific data augmentation to simulate different
conditions.
2. Outlier Management: The presence of significant outliers in energy
generation should be further investigated. Anomalous events could be due
to equipment malfunction or extreme weather conditions, and
implementing anomaly detection could help in filtering or adjusting the
model for these extremes.
3. Enhancing Data Coverage: Collecting additional data for conditions not
well-represented in the current dataset, such as seasonal extremes or rare
weather patterns, could improve the robustness of the model.
By addressing these areas, DAC Green Energy Company can optimize its energy
production efficiency, reduce operational uncertainties, and contribute to its
sustainable energy goals

# REFERENCE
[1] J. Jevšenak, M. SkudnikA random forest model for basal area increment predictions
from national forest inventory data,Ljubljana, Slovenia 2021
[2] J. L. Rosenberg och L. M. Epstein, Schaum's Outline of College, New York:
McGRAW - HILL, INC, 2000. .
[3] L. Prokhorenkova, G. Gusev, A. Vorobev, A.V. Dorogush, A. Gulin,
CatBoost: unbiased boosting with categorical features, ADVANCES IN
[3] NEURAL INFORMATION PROCESSING SYSTEMS 31 (NIPS 2018),
(2018) 6638-6648
[4] Prokhorenkova L, Gusev G, Vorobev A, Dorogush AV, Gulin A. CatBoost:
unbiased boosting with categorical features.n.d.. 2018
[5] Y. Shabing., H. Qian,Mean squared error bound for learning-based multi-target
localization and its application in learning network architecture design. 2024

# CITATION
CS DAC 2024. (2024). Preliminary Round DAC PRS 2024. Kaggle. https://kaggle.com/competitions/preliminary-round-dac-prs-2024












