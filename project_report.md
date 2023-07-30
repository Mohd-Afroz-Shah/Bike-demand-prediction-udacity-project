# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### SHAH MOHD AFROZ GULAM SAMDANI


## Initial Training
##  Attempts made to submit my predictions, learning and adjustments values
When showed that Kaggle excluded submissions having negative values in the predictions during the initial training. This need was met by implementing a post-processing step to adjust any negative anticipated values to zero before submission. This avoided any predictions from being rejected because of negative values and made sure the predictions followed Kaggle's submission standards. The pipeline included a post-processing step to ensure successful Kaggle submissions and to ensure that the predictions adhered to the platform's rules.

### Performance of best model among?
The WeightedEnsemble_L2 model, notably the added features model, came out on top in this project. On the test dataset, it received the highest Kaggle score of 0.55438. Without using a hyperparameter optimisation process, this model was created by training on data that had undergone exploratory data analysis and feature engineering. This particular model performed the best on the unseen test dataset, but some models showed increased RMSE scores on the validation data after hyperparameter optimisation. It is important to note that numerous models offered competitive performance, and the best model was chosen after taking into account both the Kaggle scores on the test dataset and the RMSE scores obtained during cross-validation.


## Exploratory data analysis
The datetime feature was parsed to extract the hour information. Categorical variables were converted to category data types. Feature extraction created independent features. The casual and registered features, though correlated, were ignored due to their absence in the test data. A new categorical feature, day_type, categorized weekdays, weekends, and holidays. To reduce multicollinearity, atemp was removed. These steps improved the dataset for model training and analysis.


### How model perform after adding additional features ?
The model's performance considerably increased once the extra "hour" function was added. Better predicted accuracy is seen by the Kaggle score dropping from  0.55438  to 0.49469. With the addition of the "hour" element, the model was able to better reflect the effects of time of day on demand for bike sharing.


## Hyperparameter tuning
### How much better did your model preform after trying different hyper parameters?
The model's performance increased further after hyperparameter optimisation. The top-ranked model received the highest Kaggle score of all the models trained for the experiment, 0.50090 


### Create a table with the models.
| Model                       | hpo1                  | hpo2                | hpo3                        | Score    |
|-----------------------------|-----------------------|---------------------|-----------------------------|----------|
| initial                     | prescribed_values     | prescribed_values   | presets: 'best quality'    | 1.80210   |
| add_features                | prescribed_values     | prescribed_values   | presets: 'best quality'    | 0.44632   |
|hpo (top-hpo-model: hpo1) |  Tree-Based Models: (GBM, XT, & XGB)|LightGBMXT|"presets: 'optimize_for_deployment"| 0.50090 |

### Graph of result

![image](https://github.com/Mohd-Afroz-Shah/Bike-demand-prediction-udacity-project/assets/98610550/81761195-c1a4-4141-ba83-e83de29d18f7)

## Summary
In this task, I utilised AutoGluon to project demand for bike sharing. After the initial training, I recognised that negative projected values required to be set to zero in order for the submission to be successful. The best model, with a Kaggle score of 0.50090, was generated through hyperparameter optimisation. Exploratory analysis was used to determine the significance of the "hour" variable, which significantly improved the model's performance. If given more time, it may be possible to research additional feature engineering and hyperparameter tuning to enhance the model's accuracy.

