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



