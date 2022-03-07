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

Additional correlation analysis including newly created features shows a perfect correlation between the cosine and sine of date features than their actual values (Month and Hour). Hence, Month and Hour features are dropped in the modeling process.

## Data splitting

Declaring feature vector and target variables, entire dataset is split into 70% training data and 30% test data. 

## Feature Selection - Dropping features using Pearson Correlation 
![download](https://user-images.githubusercontent.com/81407869/156967485-cd335407-eb16-434a-9d26-2230d8cdc444.png)






