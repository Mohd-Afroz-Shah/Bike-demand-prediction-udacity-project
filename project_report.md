# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### SHAH MOHD AFROZ GULAM SAMDANI


## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
**Five different experiments were performed as follows:**
1. Initial Raw Submission   **[Model: `initial`]**
2. Added Features Submission *(EDA +  Feature Engineering)* **[Model: `add_features`]**
3. Hyperparameter Optimization (HPO) - Initial Setting Submission 
4. Hyperparameter Optimization (HPO) - Setting 1 Submission **[Model: `hpo (top-hpo-model: hpo1)`]**

**Observation:** While submitting predictions obtained from all these five experiments, some of the experiments delivered negative predictions values.<br>
**Changes incorporated:** Kaggle refuses the submissions containing negative predictions values obtained from the predictor. Hence, all such negative outputs from respective predictors were replaced with 0.<br>


### What was the top ranked model that performed?
The top-ranked model in this project was the WeightedEnsemble_L3 model, specifically the add features model. It achieved a validation root mean squared error (RMSE) score of 34.2609 and the best Kaggle score of 0.44956 on the test dataset. This model was developed by training on data that underwent exploratory data analysis (EDA) and feature engineering without the use of a hyperparameter optimization routine. While some models showed improved RMSE scores on the validation data after hyperparameter optimization, this particular model demonstrated the best performance on the unseen test dataset. It is worth noting that several models delivered competitive performance, and the selection of the top model considered both the RMSE scores during cross-validation and the Kaggle scores on the test dataset.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
- Feature `datetime` was parsed as a datetime feature to obtain hour information from timestamp
- Independent features `season` and `weather` were initially read as `integer`. Since these are categorical variables, they were transformed into `category` data type.
- The data for `year`, `month`, `day` *(dayofweek)* and `hour` were extracted as distinct independent features from the `datetime` feature using feature extraction. Upon feature extraction, `datetime` feature was dropped. 
- After probing and considering the features, `casual` and `registered`, it was noticed that the RMSE scores improved significantly during cross-validation and these independent features were highly co-related to the target variable `count`. However, the features `casual` and `registered` are only present in the train dataset and absent in the test data; hence, these features were ignored/dropped during model training
- Another categorical feature `day_type` was added based on `holiday` and `workingday` feature. It was defined to effectively segregate "weekday", "weekend" and "holiday" categories.
- Moreover, features `temp` (temperature in degree Celsius) and `atemp` (*'feels like'* temperature in degree Celsius) had a `high positive correlation of 0.98`. Hence, in order to reduce multicollinearity between independent variables, `atemp` was dropped from the train and test datasets respectively.
- Further, data visualization was conducted to derive insights from the features.


### How much better did your model perform after adding additional features and why do you think that is?
-The inclusion of additional features resulted in a significant improvement of approximately 138% in model performance compared to the initial/raw model that did not undergo exploratory data analysis (EDA) or feature engineering.
-Converting certain categorical variables from integer data types to their true categorical data types contributed to the enhanced model performance.
-During model training, the features "casual," "registered," and "atemp" were ignored. Additionally, "atemp" was dropped due to its high correlation with another independent variable, "temp." This step helped reduce multicollinearity in the model.
-The "datetime" feature was split into multiple independent features, including "year," "month," "day," and "hour." Additionally, a new feature called "day_type" was added. These predictor variables enabled the model to effectively assess seasonality or historical patterns in the data, leading to further improvements in model performance. 


## Hyperparameter tuning
### How much better did your model preform after trying different hyper parameters?
Hyperparameter tuning proved to be beneficial as it improved the model's performance compared to the initial submission. Three different configurations were tested during the hyperparameter optimization experiments. While the hyperparameter-tuned models achieved competitive performances, they were outperformed by the model that incorporated exploratory data analysis (EDA) and additional engineered features when evaluated on the Kaggle test dataset.

**Observations:**
-Considered the prescribed settings while utilizing the autogluon package for training, but the performances of hyperparameter optimized models were sub-optimal.
-Hyperparameters were tuned with a fixed set of values provided by the user, limiting the options that autogluon could explore.
-The 'time_limit' and 'presets' parameters played a crucial role in hyperparameter optimization using autogluon.
-Insufficient time limit for model building could lead to autogluon failing to build any models for the prescribed set of hyperparameters.
-Presets such as "high_quality" with auto_stack enabled required high memory usage and were computationally intensive within the given time limit and available resources.
-Experimentation with lighter and faster preset options like 'medium_quality' and 'optimized_for_deployment' was conducted.
-The faster and lighter preset, "optimized_for_deployment," was preferred for the hyperparameter optimization routine as other presets failed to create models using AutoGluon for the experimental configurations.
-Balancing the trade-off between exploration and exploitation poses a significant challenge when using AutoGluon with a prescribed range of hyperparameters.


### If you were given more time with this dataset, where do you think you would spend more time?
Given more time to work with this dataset, I would like to investigate additional potential outcomes when AutoGluon is run for an extended period with a high quality preset and enhanced hyperparameter tuning.


### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|prescribed_values|prescribed_values|"presets: 'best quality'"|1.80520|
|add_features|prescribed_values|prescribed_values|"presets: 'best quality'"|0.44956|
|hpo (top-hpo-model: hpo1)|Tree-Based Models: (GBM, XT, & XGB)|LightGBMXT|"presets: 'optimize_for_deployment"|0.49440|


### Create a line plot showing the top model score for the three (or more) training runs during the project.

![image](https://github.com/Mohd-Afroz-Shah/Bike-demand-prediction-udacity-project/assets/98610550/1bf12f71-2685-4198-b1fa-e2f189d4b5f2)(img/model_train_score.png)


### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![image](https://github.com/Mohd-Afroz-Shah/Bike-demand-prediction-udacity-project/assets/98610550/719202a0-eded-4b8f-a03b-ef330e16b1c7)(img/model_test_score.png)


## Summary
-Through study and incorporation of the AutoGluon AutoML framework for Tabular Data in a bike sharing demand prediction project.
-Utilization of AutoGluon's capabilities for automated stack ensembling and individually configured regression models on tabular data.
-Quick prototyping of a baseline model with the help of the AutoGluon framework.
-Significant improvement in results by the top-ranked AutoGluon-based model, which utilized data obtained after extensive exploratory data analysis (EDA) and feature engineering without hyperparameter optimization.
-Leveraging automatic hyperparameter tuning, model selection/ensembling, and architecture search to explore and exploit the best possible options using AutoGluon.
-Improved performance through hyperparameter tuning using AutoGluon, but not better than the model with EDA, feature engineering, and no hyperparameter tuning.
-Hyperparameter tuning with AutoGluon noted to be a cumbersome process, heavily dependent on factors such as time limit, prescribed presets, model families, and range of hyperparameters to be tuned.
