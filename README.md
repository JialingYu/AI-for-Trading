# Artificial Intelligent for Trading
This is a github repo containing my notes and the projects that I've done for the Udacity nano degree program 'AI for trading'.



## 7. Combining Signals for Enhanced Alpha

### Decision tree: 

separate the data sets into two sets according to some attribute of the data set so that the separation has the largest information gain.

Advantages: easy to interpret, require little data preparation, can handle many datatypes and large data set

Disadvantage: low prediction accuracy, prone to overfitting

Advantages of tree based method in financial analysis:
no need to scale input data, robust to outlier, missing values and noisy data


### Random forest:
[Using random forest to predict whether a text message is spam or not](decision tree and random forest/spam_randomforest.ipynb)

### Feature engineering

Features are generalization of alpha factors. Alpha facotrs are signals that are idealy predictive of whether future stock returns are positive or negative, and by how much. A feature does not need to be predictive by itself as alpha factor, but can be used to combined other features or alpha factors for prediction, which means features are conditional factors. For example, the conditional factor idiosyncratic volatility on it own do not predict future return, but when combined with other factors it can be predictive.

#### Universal quant features: stock volatility and stock dollar volumn. 

Both of them can be used as a conditional factor to adjust the impact of other feature factors. For example, high dollar volumn over a period of time may indicate that some momentum factor is more significant compared to when there is lower dollar volumn.

#### Market Regime Feature:

##### Market Dispersion: the standard deviation of the cross section of all stocks on each day.


If the dispersion is low, the stocks move in the same direction. If the dispersion is high, the stocks move in different directions, and we pay more attention to the idiosyncratic factor of each stock instead of the common factors of all stocks.

##### Market volatility: the volatility of a stock universe over a time horizon

Varying level of market volatility may affect how the stock selection startegy perform.

During period of high market volatility, a mean reversion factor maybe more relevant to future return, while during period of low market volatility, fundamental factor may ber more relevant. A possible reason is that when market is volatile, market participant tend to trade more, which drives the market to theopposite direction fo the demand. And when the market is stable, the fundamental factor of the companies does not covered by the mean reversion factor and thus stands out.

#### Sector and Industry

Sector is a major factor that affects stock movement. The sector or industry classification of a stock can also be used as a feature, since stocks in the same sector tend to move together and certain alpha factors can be relevant to not relevant according to sectors. For example, a value factor does not make much sense for a bank since banks are not valued in the same way as other companies.


