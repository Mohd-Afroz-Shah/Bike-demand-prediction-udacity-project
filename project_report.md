# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### SHAH MOHD AFROZ GULAM SAMDANI


## Initial Training
## When you attempted to submit your predictions, what did you learn? What adjustments to the predictor's output were necessary for you to submit your findings?
When showed that Kaggle excluded submissions having negative values in the predictions during the initial training. This need was met by implementing a post-processing step to adjust any negative anticipated values to zero before submission. This avoided any predictions from being rejected because of negative values and made sure the predictions followed Kaggle's submission standards. The pipeline included a post-processing step to ensure successful Kaggle submissions and to ensure that the predictions adhered to the platform's rules.

### Performance of best model among?
The top-ranked model in this project was the WeightedEnsemble_L2 model, specifically the add features model. It achieved the best Kaggle score of 0.55438 on the test dataset. This model was developed by training on data that underwent exploratory data analysis (EDA) and feature engineering without the use of a hyperparameter optimization routine. While some models showed improved RMSE scores on the validation data after hyperparameter optimization, this particular model demonstrated the best performance on the unseen test dataset. It is worth noting that several models delivered competitive performance, and the selection of the top model considered both the RMSE scores during cross-validation and the Kaggle scores on the test dataset.

## Exploratory data analysis
The datetime feature was parsed to extract the hour information. Categorical variables were converted to category data types. Feature extraction created independent features. The casual and registered features, though correlated, were ignored due to their absence in the test data. A new categorical feature, day_type, categorized weekdays, weekends, and holidays. To reduce multicollinearity, atemp was removed. These steps improved the dataset for model training and analysis.


### How much better did your model perform after adding additional features and why do you think that is?
The model's performance considerably increased once the extra "hour" function was added. Better predicted accuracy is seen by the Kaggle score dropping from  0.55438  to 0.49469. With the addition of the "hour" element, the model was able to better reflect the effects of time of day on demand for bike sharing.


## Hyperparameter tuning
### How much better did your model preform after trying different hyper parameters?
The model's performance increased further after hyperparameter optimisation. The top-ranked model received the highest Kaggle score of all the models trained for the experiment, 0.50090 

### Create a table with the models you ran, the hyperparameters modified, and the Kaggle score.
| Model                       | hpo1                  | hpo2                | hpo3                        | Score    |
|-----------------------------|-----------------------|---------------------|-----------------------------|----------|
| initial                     | prescribed_values     | prescribed_values   | presets: 'best quality'    | 1.80210   |
| add_features                | prescribed_values     | prescribed_values   | presets: 'best quality'    | 0.44632   |
|hpo (top-hpo-model: hpo1) |  Tree-Based Models: (GBM, XT, & XGB)|LightGBMXT|"presets: 'optimize_for_deployment"| 0.50090 |

### Graph of result

![image](https://github.com/Mohd-Afroz-Shah/Bike-demand-prediction-udacity-project/assets/98610550/81761195-c1a4-4141-ba83-e83de29d18f7)

## Summary
In this project, I forecast demand for bike sharing using AutoGluon. I started with the initial training and realised that for a successful submission, negative predicted values needed to be set to zero. Hyperparameter optimisation led to the top-ranked model, which received a Kaggle score of 0.50090. The "hour" feature's significance was discovered through exploratory analysis, which greatly enhanced the model's performance. Additional feature engineering and hyperparameter tuning could be investigated to improve the model's accuracy if given additional time.

