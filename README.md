# Unit-10-Homework
## A Yen for the Future
### Return Forecasting: Time Series Analysis & Modelling with CAD-JPY Exchange rate data
After importing the required libraries and reading the csv file, I trimmed the dataset so that it would begin from the date specified in the instructions: January 1, 1990.  
Initial plot showing the Settle price: <br />
![image](https://user-images.githubusercontent.com/93611442/151679866-98a0ac66-ed1c-4747-9bc8-df032dbdbdff.png)  
We can see a downward trend and that the time series is non-stationary.    
Then I decomposed the exchange rate price into trend and noise using a Hodrick-Prescott Filter and put the results in a new dataframe:  
![image](https://user-images.githubusercontent.com/93611442/151679835-c2241560-3d4b-4ef6-ad46-ef5754e78bae.png)  
Exchange Rate Price vs. the Trend for 2015 to the present:  
![image](https://user-images.githubusercontent.com/93611442/151679933-f1d884ff-21da-42c0-8416-d2795ca63bc9.png)  
We can see a major downward trend until the end of 2016 following by an almost cosolidation until early 2020 and then a downward trend again.  
The Settle Noise:  
![image](https://user-images.githubusercontent.com/93611442/151680013-b3a58315-f8e9-4bc8-85cf-48e8803faf6e.png)  

### Forecasting Returns using an ARMA Model
After calculating the returns, I created an ARMA(2,1) model (using statsmodels.api library). The following is the summary table:   
![image](https://user-images.githubusercontent.com/93611442/151680166-4f441800-4494-408b-af14-e61b2b34a121.png)  
And the 5 Day Returns Forecast:  
![image](https://user-images.githubusercontent.com/93611442/151680231-01247a99-f264-4e89-8c12-a2615e3d1cc8.png)  
Based on the p-values, only 2 of the coefficients are statistically significant (AR_1 and ML_1), which means this model is not a good fit. This is what we expected, as the time series we have is "non-stationary".  

### Forecasting the Exchange Rate Price using an ARIMA Model
Then I estimated an ARIMA(5,1,1) model, using ARIMA function from statsmodels.tsa.arima_model. The following is the summary table:  

![image](https://user-images.githubusercontent.com/93611442/151680324-71047e80-40ba-41e2-9648-7841a96ad4eb.png)  
And the 5 Day Price Forecast:  
![image](https://user-images.githubusercontent.com/93611442/151680343-3c64877b-d1de-4326-b3d7-9adaaf252533.png)  
Based on the model predictions, we can expect Japanese Yen's value to drop by more than 0.08.  

 ### Volatility Forecasting with GARCH
 In this section instead of predicting returns, near-term **volatility** of Japanese Yen exchange rate returns is forecasted.  
 I created a GARCH(2,1) model, using the arch library, and fitted it to the returns data from the ARMA section.  
 Here are the results:  
 ![image](https://user-images.githubusercontent.com/93611442/151680480-39afc5b0-726f-4b97-a6c6-53980045f75d.png)  
 The p-values for GARCH and volatility forecasts tend to be much lower than our ARMA/ARIMA return and price forecasts. We have all p-values of less than 0.05, except for alpha(2), indicating overall a much better model performance.  
 The final forecast plot:  
 ![image](https://user-images.githubusercontent.com/93611442/151680549-c925f711-edda-4606-b051-f840c15e93f2.png)  
 The model predicts that the volatility will be increasing with a constant rate.  
 
 ### Conclusions
 1. Based on your time series analysis, would you buy the yen now?

    * No. Based on the price and the volatility forecast, it is not a good time to buy Yen.  
 2. Is the risk of the yen expected to increase or decrease?
    * It is expected to increase.  
 3. Based on the model evaluation, would you feel confident in using these models for trading?
    * Yes; we can certainly understand the trends/patterns of the market better. However, since these models use historic data, none of them could be 100% accurate in predicting the future.











