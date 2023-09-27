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

#### Universal Quant Features: stock volatility and stock dollar volumn. 

Both of them can be used as a conditional factor to adjust the impact of other feature factors. For example, high dollar volumn over a period of time may indicate that some momentum factor is more significant compared to when there is lower dollar volumn.

#### Market Regime Feature:

##### Market Dispersion: the standard deviation of the cross section of all stocks on each day.


If the dispersion is low, the stocks move in the same direction. If the dispersion is high, the stocks move in different directions, and we pay more attention to the idiosyncratic factor of each stock instead of the common factors of all stocks.

##### Market volatility: the volatility of a stock universe over a time horizon

Varying level of market volatility may affect how the stock selection startegy perform.

During period of high market volatility, a mean reversion factor maybe more relevant to future return, while during period of low market volatility, fundamental factor may ber more relevant. A possible reason is that when market is volatile, market participant tend to trade more, which drives the market to theopposite direction fo the demand. And when the market is stable, the fundamental factor of the companies does not covered by the mean reversion factor and thus stands out.

#### Sector and Industry

Sector is a major factor that affects stock movement. The sector or industry classification of a stock can also be used as a feature, since stocks in the same sector tend to move together and certain alpha factors can be relevant to not relevant according to sectors. For example, a value factor does not make much sense for a bank since banks are not valued in the same way as other companies.

#### Date 

Date can be an important factor for forward return. For example, during the start and end of each day, month, year, the stock market will have some irregular behaviour due to human factor.

### Overlapping labels

An important problem when using machine learning algorithm on financial data is that the data are correlated. For example, if we use the weekly returns as labels, they are correlated since the data used to calculate the weekly return of neighboring days are overlapped. And we know that for supervised machine learning algorithm it is important that the training data are independent identically distributed, so that the model can have good generalization. For example, when we use random forest, it is important that the data are i.i.d so that the trees that we generate are different. For correlated data, we can only generate correlated trees, which would increase the rate of classification error meade by the forest. In addition, when peerforming out of bag testing, the data that we used to test are also correlated with the data that we used to train, and thus inflate the performance of the random forest on the testing data.

**Solutions** [solving overlapping labels](decision tree and random forest/dependent_labels.ipynb)
- only use unoverlapped data
- use a smaller bag of data
- separate the data into unoverlapped groups, train classifiers on each group separately and ensemble them together.

### Feature importance

[Feature importance method in sci-kit learn](calculate_shap,ipynb)

[implement the simple version of the Tree Shap algorithm](tree_shap.ipynb)


