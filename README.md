# High Frequency Trading Algorithm - Optional 

![[cover.jpg]](Images/cover.jpg)

Due to the volatility in investment performance of human portfolio managers, many investment firms rely on trading algorithms to produce consistent investment performance capable of outperforming the markets. One such investing strategy is the combination of Machine Learning Algorithms and High Frequency Algorithms. This strategy has become very popular and requires skills from multiple of the previous units, such as automatically retrieving data used to make investment decisions, training a model, and building an algorithm to execute the trading.

I have been tasked by the investment firm Renaissance High Frequency Trading (RHFT) to develop such an algorithm. RHFT wants the algorithm to be based on stock market data for `FB`, `AMZN`, `AAPL`, `NFLX`, `GOOGL`, `MSFT`, and `TSLA` at the minute level. It should conduct buys and sells every minute based on 1 min, 5 min, and 10 min Momentum. The CIO has asked me to choose the Machine Learning Algorithm best suited for this task and wants these executed via Alpaca's API.

I have competed the following:

1. [Prepare historical return data for training and testing (optional)](#part-1-prepare-the-data-for-training-and-testing-optional)


2. [Compare prediction performance of multiple ML-Algorithms](#part-2-train-and-compare-multiple-Machine-Learning-Algorithms)


3. [Implement a fully functional trading algorithm that buys and sells the stocks selected by the Model](#part-3-implement-the-strongest-model-using-alpaca-api)



### Part 1: Prepare the data for training and testing (optional)


#### Data Generatation

The following shows the DataFrame returned from the Alpaca API containing only close prices.

![[df_closing_prices]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/df_closing_prices.PNG?raw=true)


#### Computing Returns

The following shows percent change computed at 1 min intervals

![[df_returns]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/df_returns.PNG?raw=true)


The following shows the 1, 5, and 10 minute momentums that will be used to predict the forward returns

![[df_momentums]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/df_momentums.PNG?raw=true)



### Part 2: Train and compare multiple Machine Learning Algorithms

#### Preprocessing Data

Data has been split into testing and training sets using shuffle = False. From there the data has been resampled ready for modelling. 

![[resampled]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/resampled.PNG?raw=true)



#### Machine Learning

The performance of the 5 different machine learning algorithms has been evaluated and the LogisticRegression model has been chosen as it has the highest accuracy.

- 1a Which model produces the highest Accuracy?     
    - **0.527809939034318 - LogisticRegression**
    - 0.5001718617146371 - RandomForestClassifier
    - 0.5098051630877218 - GradientBoostingClassifier
    - 0.4875671617490095 - AdaBoostClassifier
    - 0.5123785661305787 - XGBClassifier
    
        **Answer the LogisticRegression model produces the highest accuracy**     
    
- 1b Which model produces the highest performance over time?
    - **0.5278 - LogisticRegression**
    - 0.4955 - RandomForestClassifier
    - 0.5098 - GradientBoostingClassifier
    - 0.4841 - AdaBoostClassifier
    - 0.5089 - XGBClassifier
    
        **Answer the LogisticRegression model produces the highest performance over time** 

- 1c Which model produces the highest Sharpe Ratio?
    - 0.9954988518686781 - LogisticRegression
    - 0.7687061147858075 - RandomForestClassifier
    - 1.0136266691392073 - GradientBoostingClassifier
    - **1.1689944579443594 - AdaBoostClassifier**
    - 0.8345229603962802 - XGBClassifier
    
        **Answer the AdaBoostClassifier model produces the highest Sharpe Ratio** 


### Part 3: Implement the strongest model using Alpaca API

In this final section, I have created the algo-trading program by pulling live data at the minute frequency and ensuring that the model is buying the selected stocks. 

#### Develop the Algorithm

Using the data from the API and the best machine learning algorithm as determined above, the following buy predictions have been determined. Included are the buy stock tickers, the total available capital, the capital per stock and the iteration through the buy_dict to determine the number of shares to buy.

![[buy_dict]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/buy_dict.PNG?raw=true)


#### Automate the Algorithm

A trade function has been created to automate the end to end process of trading using this algorithm. Using the schedule model the algorithm has been scheduled to run ever minute at 5 seconds past the minute. The algorithm uses the Alpaca API to check if the market is open and will only trade when the market is open. 


![[schedule]](https://github.com/apfreeman/Unit-15-High-Frequency-Trading-Algorithm/blob/main/Images/schedule.PNG?raw=true)

