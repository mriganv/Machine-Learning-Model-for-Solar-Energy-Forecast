# Machine-Learning-Model-for-Solar-Energy-Forecast
## About

This is a short data science project about developing a machine learning regression model to accurately predict the rate of solar output measured as a % of baseline of capacity. 

## Data 

The model is trained using real data obtained from three sources 
* A dataset which measures the rate of solar output measured as a % of baseline of capacity between 2014 and 2018, collected from real-life example. 
* Weather dataset from an API call to www.worldweatheronline.com for Hanover, Massachusetts location between  2014 and 2018. 
* Solar Irradiance datasets from www.nsrdb.nrel.gov between 2014 and 2018, which includes data on solar and weather values for variables such as Global Horizontal Irradiance (GHI), Direct Horizontal Irradiance (DHI), Direct Normal Irradiance (DNI), Wind Speed, Temperature and Solar Zenith Angle downloaded from the NSRDB. 

## Data Processing
Available vaiables in the data are explored, visualized and pre-processed before being passed to the machine learning algorithms. 

Data Exploration

After carefully removing certain columns, dataset consists of 20571 entries with total 38 columns. 
![Screenshot 2022-03-06 191400](https://user-images.githubusercontent.com/81407869/156961669-a381e4ce-17e2-41d4-b772-ae84bc9b1041.jpg)
Further deleted minute column. 

As shown above, there are no missing values in the dataset. The target variable is % baseline.
![Screenshot 2022-03-06 193758](https://user-images.githubusercontent.com/81407869/156963788-17b77bab-9097-46a5-a5b8-424662a240e3.jpg)

From the correlation plot, sunHour, tempC, FellslikeC, HeadIndexC, WindChillC, humidity, DNI, Cloud Type, Solar Zenith Angle, Cloudcover are some of the correlated features with % baseline. 

## Feature Engineering

From the above correlation plot, we can see that hour variable is not related to the target variable. Lets create cyclic features using month and hour data. 

![Screenshot 2022-03-06 200645](https://user-images.githubusercontent.com/81407869/156966605-43b566f5-36b3-40be-a1f0-a93fd7e8f41e.jpg)


![Screenshot 2022-03-06 200708](https://user-images.githubusercontent.com/81407869/156966621-3bf8a620-ee29-4d41-8835-44f468c0a756.jpg)

![download (1)](https://user-images.githubusercontent.com/81407869/156968574-6ac5d0c3-cd39-476b-9126-52096e9c4873.png)

Additional correlation analysis including newly created features shows a perfect correlation between the cosine and sine of date features than their actual values (Month and Hour). Hence, Month and Hour features are dropped in the modeling process.

## Data splitting

Declaring feature vector and target variables, entire dataset is split into 70% training data and 30% test data. 

## Feature Selection - Dropping features using Pearson Correlation 
![download](https://user-images.githubusercontent.com/81407869/156967485-cd335407-eb16-434a-9d26-2230d8cdc444.png)

When you have two independant variables that are very highly correlated, then definitely we should remove one of them because two variables are so highly correlated they will obviously impart nearly exactly the same information to your regression model. By including both you are actually weakening the model.You are not adding incremental information. Instead, you are infusing your model with noise. Not a good thing.

![Screenshot 2022-03-06 204543](https://user-images.githubusercontent.com/81407869/156969625-7e4de6da-15ac-43c3-9e43-a1c7cc1a7ee9.jpg)

Based on the Pearson correlation, we are selection columns which are having correlation greater than 0.9 and making a list of those columns to drop. 
Droping the columns which are in the list from the training and testing dataset. 


![Screenshot 2022-03-06 204728](https://user-images.githubusercontent.com/81407869/156969749-dc43b6fb-f795-4a23-815f-4a2b8f5985cb.jpg)

## Modeling

Three Models (Linear Regression, Stacked Ensemble Model and Light Gradient Boosting Machine — LGBM) were developed. 

## Model Results:


### Linear Regression Model:



![Screenshot 2022-03-06 205847](https://user-images.githubusercontent.com/81407869/156970726-3249d7cb-a0a6-4c19-a2a4-7f7de9998cd7.jpg)


![Screenshot 2022-03-06 205921](https://user-images.githubusercontent.com/81407869/156970788-b54e608f-85ba-48bb-9cf1-34336edc878c.jpg)

### Stacked Enesemble Model:

Hyper-parameter tuning

Each of the models was tuned using the random search cross-validation approach which enables the selection of the best combination of hyper-parameters based on the performance of the model on multiple splits of the training data.
In particular, 1000 permutations of the hyper-parameters were chosen and applied to 4 splits of the training data. The test data remains unseen and will be used for the final evaluation of the models chosen across different algorithms.

![3-fold-cross-validation-and-final-test-diagram-The-dataset-was-divided-into-four](https://user-images.githubusercontent.com/81407869/156971048-8deec5d7-25fe-4978-979c-6e70bd1b0a78.png)

Model stacking
Four disparate models (KNN, DNN, RF, and LGBM) were combined using the stacking regressor module in Scikit-learn- python machine learning library. A simple linear regression model was used as the meta-learner and it was trained on 4 fold cross-validated predictions of the base models as well as the original input features.
The stacking regressor uses the cross_val_predict function which returns for each example in the training data, the prediction that was obtained for that example when it was in the validation set. These predictions across the different base models are used as an input to the meta-learner. This approach reduces the risk of overfitting.


![Stacking-model-1-S1](https://user-images.githubusercontent.com/81407869/156971346-4c55614e-26a5-48fb-80a5-f5c06e20bfee.png)

#### Model Performance of Stacked Ensemble model on test set
![Screenshot 2022-03-06 210819](https://user-images.githubusercontent.com/81407869/156971677-72ac32c2-06e0-40f0-aead-4a8d100b7413.jpg)

###  Light Gradient Boosting Machine — LGBM

### LGBM  Model Results



![Screenshot 2022-03-06 211238](https://user-images.githubusercontent.com/81407869/156971998-ec7a0b55-da3e-4c57-996d-56c1332c4027.jpg)

### Conclusions:

Stacked Ensemble Model and LGBM gave an overall best performance with 92% than the Linear Regression Model(73%). 


