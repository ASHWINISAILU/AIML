**Analysis of Factors Affecting Flight Delay using the Machine learning - Python**


**Abstract**

Flight delays are a critical challenge in the aviation industry, impacting both operational efficiency and passenger satisfaction. This study analyzes factors contributing to flight delays using a dataset of U.S. airline operations spanning August 2013 to August 2023. Various delay types, including carrier-related, weather-related, and NAS (National Airspace System) delays, are examined. Data preprocessing steps such as handling missing values, outlier detection, and encoding categorical variables are performed to ensure data integrity. Exploratory Data Analysis (EDA) reveals key correlations between different delay factors. Machine learning models, including Linear Regression, Gradient Boosting Regression, and LightGBM, are implemented to predict arrival delays. LightGBM outperforms other models with the lowest Mean Squared Error (MSE) and highest predictive accuracy. The study identifies arr_del15, late_aircraft_delay, and carrier_delay as the most significant contributors to flight delays. Based on the findings, recommendations for improving airline operations and future research directions are proposed to minimize delays and enhance air travel efficiency.

**1. Introduction**

Flight delays are a significant issue in air transportation, causing inconvenience to passengers and operational challenges for airlines. This study aims to analyze the factors influencing flight delays using a dataset covering U.S. carrier performance from August 2013 to August 2023. The insights derived from this analysis can help optimize operational strategies and minimize delays.


**2. Dataset Description**

The dataset is sourced from Kaggle and contains 171,666 rows and 21 columns. It includes information on flights, delays, and attributing factors such as carrier, weather, NAS (National Airspace System), security, and late aircraft arrivals. The dataset provides details on the number of arriving flights, delays exceeding 15 minutes, cancellations, diversions, and various delay reasons.



**3. Data Preprocessing**

**Handling Missing Values:** Missing values were detected in several columns, primarily in arr_del15, arr_flights, and various delay categories. Missing values were imputed using the K-Nearest Neighbors (KNN) imputation method to retain data integrity.

![image](https://github.com/user-attachments/assets/1f6ef1dc-b071-4498-a5f3-a7303a3f3e46)


![image](https://github.com/user-attachments/assets/9cf03a38-2d0c-42fc-bd09-21c570e29b18)

The missing data values are found majority in column arr_del15 and rest are equally distributed in nas_ct, security_ct,security_delay,nas_delay,weather_delay,carrier_delay,arr_delay,arr_diverted,arr_cancelled,late_airc weather_ct,carrier_ct,arr_flights. Columns month,airport_name,airport,carrier_name_carrier,year has no null values. As part of data preprocessing, removing the missing values is important to streamline the data, and avoid data manipulation, the sample size for training data, and uninterrupted values across the dataset to avoid any further model failures or nonresponsiveness. Since the dataset is persistent and numeric and there exists a relationship between different variables(columns), lost values are not regularly dispersed, The KNN ascription strategy is utilized to fill within the lost values within the dataset. This makes the dataset more optimized and can handle skewed conveyed information. KNN ascription strategy calculates the values of a lost information point based on the values of its closest neighbors on include arrange.

**Outlier Detection & Treatment: **The Winsorizing technique was used to cap extreme values and reduce skewness in the data.

**Label Encoding: ** Categorical variables like carrier, carrier_name, airport, and airport_name were converted into numeric form for analysis.

![image](https://github.com/user-attachments/assets/afcb515e-b192-4287-b411-67f73710b4e5)

![image](https://github.com/user-attachments/assets/91e230fb-0839-45d6-812d-afa4cb4103cc)

When the data is scattered in a dataset, it is very hard to analyze or interpret them, we cannot omit the outliers as they are as they impact the model performance. especially whether there exists a relationship between multiple variables. Effectively handling outliers will enhance the data quality as well as all information is preserved. The winsorizing technique has been used as the data is very sensitive and shows multivariate relationships, to handle the sensitivity of the data the extreme values of the lowest and highest 5% have been replaced with 5th and 95th percentile values.winsorized_df data frame contains the
transformed data with winsorized outliers. The boxplot shows before and after the winsorizing method used. This shows how the outliers are capped in without affecting the data quality.



**4. Exploratory Data Analysis (EDA)**

**Correlation Analysis: **

A heatmap was generated to visualize the relationships between different delay factors. 
**Key findings:**
arr_flights, carrier_ct, weather_ct, and nas_ct showed strong positive correlations with arr_delay. month and year had a weaker correlation with delays, suggesting external seasonal effects. carrier and carrier_name displayed a direct influence on delays.airport and airport_name had minimal impact on arr_delay.


![image](https://github.com/user-attachments/assets/9c0723d9-9ffc-4eff-9ffa-c51185c71099)




The above correlation matrix and heatmap show the relationship between different columns.This helps to understand the multiple relationships between the variables in the dataset.
*arr_flights,carrier_ct,weather_ct,nas_ct,late_aircraft_ct,arr_cancelled,arr_diverted,carrier_delay,wea security_delay, and late_aircraft_delay appear positive relationships with arr_delay.
*month and year have moderately moo relationships with arr_delay, demonstrating that they might not have a solid direct relationship with the target variable.
*carrier and carrier_name appear direct relationships with arr_delay, proposing that the carrier working the flight may impact delays.
*airplane terminal and airport_name have frail relationships with 'arr_delay', showing that the particular air terminal might have a constrained coordinate affect on delays.



**Visualization Findings:**

Airports experiencing the highest average delays were identified.

![image](https://github.com/user-attachments/assets/f0f9bce2-332a-4bb9-87c6-1924089fb8ff)


The above graph shows the pattern of average arrival delay of flights in airports across the years 2013 to 2023. There exists a continuous, seasonal pattern exists across the airports.


![image](https://github.com/user-attachments/assets/fb2a6bd3-3516-4223-91c9-d49953b56025)



![image](https://github.com/user-attachments/assets/10cfd01f-d819-474c-95da-f39f1c8bc22f)



Fig 8 shows when the number of arrival flights is higher there is a high delay in arrival as well. This clearly shows that the airports face operational congestion when the number of arrival flights is high causing a delay in arrival flights. This clearly shows the need for improvement and extra caution of the operational team in the airport during a high number of arriving flights.

Monthly and yearly trends showed fluctuating flight delays, with 2023 recording the highest delays and 2020 the lowest.


![image](https://github.com/user-attachments/assets/7c3c1bc0-7eb5-40cd-b843-3ca7942abf41)

Fig 9 shows the number of arrival flights over 10 years. There is no common trend found over 10 years. The pattern looks highly unpredictable and many other factors also influence this. The highest number of arrival flights can be seen in the years 2014 & 2019 and the least seen in 2016.

![image](https://github.com/user-attachments/assets/92e2f4c9-c468-485a-b70d-5be3317298db)

Fig 10 shows the average arrival delay every year across different airports in the U.S. In 2020 records significant low arrival delays showing good handling by the airport operational teams. And 2023 has high arrival delays in the 10 years.


![image](https://github.com/user-attachments/assets/c09eead9-e760-44e6-b49e-1497c39275ce)


Fig 11 shows the top 10 airports having the highest arrival delays. Since the airport name has undergone label encoding, they are labeled numerically. Airport 344 records the highest among all airports in the U.S.

![image](https://github.com/user-attachments/assets/86ed39f6-54f2-4c3e-a3d6-9d02df52ccb8)

Fig 12 shows a pattern over 10 years of how average flights and arrival delays are more positively correlated.

![image](https://github.com/user-attachments/assets/f4bc44d4-fc31-4799-9996-e1554fd21d71)

Fig 13 gives us an understanding of the relationship between arrival flights, arrival delay, and weather delay. This shows arrival delay cannot be influenced much due to weather delays or the number of flights.


![image](https://github.com/user-attachments/assets/4fef8a68-c3ab-4e86-9314-415030540403)

Fig 14 shows categorize the delaying factors and shows their similarities and differences. carrier delay, late aircraft delay shows more likely similar trends. NAS (National Airspace System) delay is also likely to follow the same trend. whereas weather delays and security delays completely follow different patterns.


Higher numbers of arriving flights resulted in increased arrival delays, indicating congestion at busy airports.


![image](https://github.com/user-attachments/assets/d8257036-3225-4e10-af06-9cc29ec26a47)

Fig 15 shows the count of delays due to weather, carrier, nas, security, and late aircraft. Here carrier, NAS, and late aircraft have similar trends in delay count. will weather and security counts as delay factors stay low, more unrelated to other delay factors. This clearly shows that the factors like weather and security contribute less than the other delaying factors.
All the above analysis shows us that the dataset has continuous and multiple variables that show a relationship with each other. This helps us to understand the different delaying factors contributing to the arrival delays in the last 10 years in U.S. airports.


**Machine Learning Models**

**Linear Regression**

The linear regression model is used in this dataset to find the relationship between independent and dependent variables. The above data analysis shows various relationships among the variables. To check their relationship with arrival delay, a regression model has been used. winsorized_df is the dataset used, independent variables (features), and the dependent variable (target).Assume arr_delay is the target variable, and the rest are features.
Data has been split into training and test data 80:20 ratio to find the relationship between the feature and target variables.


Training set R-squared: 0.9948545058621906
Test set R-squared: 0.9951471676537279
Training set MSE: 106143.85674097847
Test set MSE: 97512.77871040367
Training set MAE: 100.67632031973778
Test set MAE: 98.13244243403274
Training set RMSE: 10.033759032373549
Testset RMSE: 9.906182031137563


The above metrics infer that the linear regression model performs well in predicting the arr_delay variable. The r-squared value of both the training and test set falls between the range 0 to 1 showing that the model fits the data well showing accurate predictions. The average absolute difference (MAE) between the actual and anticipated values is calculated.
The model has minimal absolute prediction errors, as seen by the comparatively low MAE values for the training and test sets. The average prediction error is measured by the square root of the mean square error or RMSE. The model's ability to produce accurate predictions is further supported by the relatively low training and test RMSE values. The low MSE and MAE value indicates the accuracy of the model and the error ratio is significantly small. This model suggests that the arr_delay is highly predicted based on the features.



![image](https://github.com/user-attachments/assets/a36b4915-586b-4f82-89b9-d33cdebd30c6)

![image](https://github.com/user-attachments/assets/d709f5fa-bb2c-4599-a18a-03b43c1dacbb)

Fig 16.1 and 16.2 show the actual vs predicted values of both the training and test data set.The red dotted line is the expected actual and predicted values of the model. All the datapoints are merged on the actual and predicted line and nearing the line leaving therequirement for model improvisation.


**Gradient Bossing Regression**

The Dataset is continuous and numeric, to improvise from the previous model, a GradientBoosting regressor has been used. This model helps to provide high predictive accuracycompared to other machine learning models for this type of data. This model helps us tostudy the complex relationship of factors impacting flight arrival delays. As part of featureselection, high and moderate correlated features to arrival delay have been selected toimprovise the close study of the factors impacting the arrival flight delays in U.S airports.


Mean Squared Error: 148550.48307113635
Training Mean Squared Error: 148030.48673014776
Test Mean Squared Error: 148550.48307113635

R-squared: 0.9926072192913005

![image](https://github.com/user-attachments/assets/2e4dcbfd-2dad-4c29-8d57-21f61263d9e5)

The Gradient boosting Regressor model shows a high R square value of 99.226% showing variance in the dependent(target) variable explained by the independent variables (features).This shows that the data fits well in the model however since the MSE scores are higher, the model requires more areas of improvement to increase the better performance. According to the GBR model fig 16 shows the important features impacting the arrival delays are delayed arrival after 15 minutes, late aircraft delay, carrier delay, nas delay, and last weather delay. This will show you which features have the most importance in the model's
predictions.


**Light GBM**

Light GBM is an effective approach to increase efficiency and scalability. Also, Light GBM has many hyperparameter tuning optimization options which will give flexibility to optimize the model more effectively. Here highly correlated features are used, excluding low correlated features. Further hyperparameter optimization is made by setting parameters with regularization techniques lamda1 and lamda2(L1 &L2), later cross-validation techniques are used to avoid the overfitting of data.

Mean Squared Error (Validation): 49546.18971146538

![image](https://github.com/user-attachments/assets/80718e99-11fd-45f4-a533-026000ded890)

The MSE value of 49546.18971146538 indicates the mean square error of the validation set. This measures the average of squares of the difference between predicted and actual values. Here MSE indicates how well the flight arrival delay is impacted by the factors in the validation set. Fig 18 shows the actual vs predicted value in each fold. the MSE value is minimized using the different hyperparameters such as number of leaves, learning rate,lamda L1&L2, n boost rounds, number of k folds, max depth, min of child samples, etc.


These hyperparameters helped to increase the performance of this model.
arr_del15: 13669386932407.934
late_aircraft_delay: 1484587445507.3223
carrier_delay: 968000488946.7969
nas_delay: 178064388102.5078
weather_delay: 53128860937.10156
late_aircraft_ct: 13480879540.691406
nas_ct: 13218490112.298828
carrier_ct: 12896243692.798828
carrier: 7958603659.699219
weather_ct: 5866860356.2109375
arr_flights: 3830384591.5039062
airport: 2598567800.40625
year: 2557867342.59375
arr_cancelled: 2358696910.1953125
month: 1800901591.8945312
arr_diverted: 1168144297.8007812
security_delay: 597116370.0
security_ct: 544681912.5


![image](https://github.com/user-attachments/assets/5bbb788a-9718-4e05-b325-8ef29f050300)

Fig 19 shows the important features impacting the arrival flight delay. This graph shows that prioritized factors and operational changes to reduce these delays will help to reduce the overall arrival flight delays in U.S. airports.


**Conclusion**


The factors highly impacting the arrival delays are arrivals after 15 minutes, followed by late aircraft delay, carrier delay, NAS delay, and least weather delay. The rest of the features do not contribute to the arrival flight delays in U.S. airports over the last 10 years. Though most of the features are multi-related. The flight and airport operation team should bring some better approach to reduce these five delaying factors which in turn reduces the overall arrival flight delays in U.S airports which will make their operational structure more effective and efficient.


The most critical factors affecting flight delays are:

arr_del15 (flights delayed by 15+ minutes)
late_aircraft_delay
carrier_delay
nas_delay
weather_delay

**Operational Improvements:**
Airlines should focus on reducing turnaround times for late aircraft arrivals.

Improved coordination in the NAS system could significantly cut delays.

Weather-related delays require better predictive measures and scheduling adjustments.

**Future Research:**

Implementing deep learning models to enhance prediction accuracy.

Expanding the dataset to include real-time data for better adaptability.

Integrating passenger load factors to understand demand-related impacts on delays.


**References**

Kaggle Dataset: [Airline Delay Data](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data)

Machine Learning Techniques: scikit-learn, LightGBM, Gradient Boosting.

Data Visualization: Matplotlib, Seaborn.

Kaggle Dataset: https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data

Machine Learning Techniques: scikit-learn, LightGBM, Gradient Boosting.

Data Visualization: Matplotlib, Seaborn.
