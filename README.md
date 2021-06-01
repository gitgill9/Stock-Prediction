# Stock Price Analysis & Prediction


## Project Goal
The goal of this project is to analyze and predict stock prices and their movements. I was fascinated with an idea that a computer program in form of a machine learning algorithm can perform such complex and computational task on its own. But the main inspiration behind this project is to compare the performance of a machine generated predictions with that of stock analysts and hedge fund managers, as facts suggest that financial specialists are struggling to beat the market from past 10-15 years.

## Why Oil & Gas Stock Prediction?
I have been working in financial industry from past four years in Alberta, Canada. As an oil-based economy Alberta has suffered most than any other province in Canada in past seven years. I decided to look at big five oil companies in North America to predict the future outcomes and see if Alberta will bank upon oil industry in future or there will be shift in trend. Stock prediction is one of quite common type of time-series analysis. But I believe most of the solutions do not take in account the financial jargons or technical analysis which makes the results quite unreliable.

## Data Source
Yahoo finance is hub of all the stock prices. I was able to find stock data of all the companies for more than 25 years. For this project I chose a past five-year window to identify patterns. Following is the snapshot of ExxonMobil data acquired from Yahoo finance:
Date tells the date of record.

- **Open** is the price of stock when market opens.
- **High** is the highest stock value on that day.
- **Low** is the lowest stock value on that day.
- **Close** is the final value of stock at time of closing.
- **Adj Close** is closing price adjusted after any dividend payable by companies.

## EDA Process
This analysis required some technical financial indicators, i.e., calculations based on stock price and volume of stock traded. As the nature of stock price itself is random and sometimes volatile, it is a good idea to use technical indicators to predict at least which direction stocks are about to move. After considering group of indicators, I decide to include following four for my analysis:
• OBV (On-Balance Volume)
• MACD(Moving Average Convergence and Divergence)
• RSI (Relative Strength Index)
• ADX( Average Directional Movement Index)
The calculations for these indicators were done in excel file to permanently store them in csv file format for later use in jupyter notebooks. Following is the schema after including the technical indicators:
As it is visible that number of columns increased almost three times after calculation of technical indicators. The Blue colored columns are the indicators used for analysis and the preceding yellow columns are used to calculate these.

### EDA Steps in Jupyter notebook:
Null values: There are some null values in every dataset at beginning as some calculations required information of price for at least 14 preceding days. We will drop all rows with any null value in them.

Duplicates: There are no duplicate rows and columns found in the dataset.

Redundant columns: Some of the columns we will not use in our modelling, but these columns are useful for future purposes, so we will not drop them, instead we will create a new dataframe that will only have the columns we need.
Now we have our dataset ready to run some models on it.

## Modeling
Initially the idea was to use ARIMA and FB Prophet, but the power of neural network convinced me to use LSTM as well.
ARIMA: The results with ARIMA were quite unrealistic as the predictions were almost matching the actual price values as there was some data leakage.

FB Prophet: Prophet is FB’s own time series model. This model takes in date and stock price. I got some decent results with Prophet but the customization is somewhat limited in this model. As Prophet calculate values on it is on and will create new columns based on that, as seen below:

LSTM: Neural network are far more capable in performing complex computations and produce more accurate results. I ran a LSTM (Long-Short Term Memory) neural network which takes in account the actual price or any technical indicator to predict the stock prices. Following are the steps:
- Set a sequence of 60, which means training data is divided into data points which are sequence of 60 past values and use this data as input to first layer, this value can be stock price or any technical indicator such as RSI.
- There are three hidden layers used before reaching the output.
- Output will be stock price, i.e., a single value.
- Optimizer and loss metrics that are used are Adam and RMSE.
- Model is fitted in the end with epoch of 50 and batch value 32.
- Test data is created which is not seen by our model before.
- Predict the prices based on test data.



## Findings
Hypothesis: Goal was to use the historical data of stocks and predict stock prices and their direction with some accuracy.

Results: I anticipated that most predicted price will be way away from actual price. This was the case with some of the results but not all of them. Some results surprised me, especially when we train our model on MACD, a special type of moving average the prices were totally out of pattern with actual prices. This proves that based on our calculation some technical indicators are more accurate than others.
Best Performing Indicator: RSI (Relative Strength Index)

## Conclusion
In the nutshell, this project shows the power of machine learning and deep learning to perform complex financial calculations. But the random nature of stock price remains a mystery as there are actually no definite pattern to it. We used technical indicators to predict the direction of stock, in which we were successful but not in all results. We can improve results by following steps:
• Increase the time of dataset, instead of 5 years we can train our data on 20 years of dataset.
• Using all other technical indicators and measuring their performances with each other. This will help in finding out the ones most useful in actual prediction.
• Lastly, we can go with reinforcement learning as an alternative to increase the learning capacity of our predicting algorithms.
• It will be a tough road, but I believe by the end of this decade we will see more automated trading systems than humans.
