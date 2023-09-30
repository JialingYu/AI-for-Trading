# Artificial Intelligent for Trading
This is a github repo containing my notes and the projects that I've done for the Udacity nano degree program 'AI for trading'.



## 7. Combining Signals for Enhanced Alpha [project notebook](projects/Combine%20Signals%20for%20Enhanced%20Alpha/project_7_starter.ipynb)

### Decision tree: 

separate the data sets into two sets according to some attribute of the data set so that the separation has the largest information gain.

Advantages: easy to interpret, require little data preparation, can handle many datatypes and large data set

Disadvantage: low prediction accuracy, prone to overfitting

Advantages of tree based method in financial analysis:
no need to scale input data, robust to outlier, missing values and noisy data


### Random forest:
[Using random forest to predict whether a text message is spam or not](decision%20tree%20and%20random%20forest/spam_randomforest.ipynb)

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

Date can be an important factor for forward return which captures trader/investor behavior due to calendar anomalies. For example, during the start and end of each day, month, year, the market will behave irregularly due to huaman factor.

### Overlapping labels

An important problem when using machine learning algorithm on financial data is that the data are correlated. For example, if we use the weekly returns as labels, they are correlated since the data used to calculate the weekly return of neighboring days are overlapped. And we know that for supervised machine learning algorithm it is important that the training data are independent identically distributed, so that the model can have good generalization. For example, when we use random forest, it is important that the data are i.i.d so that the trees that we generate are different. For correlated data, we can only generate correlated trees, which would increase the rate of classification error meade by the forest. In addition, when peerforming out of bag testing, the data that we used to test are also correlated with the data that we used to train, and thus inflate the performance of the random forest on the testing data.

**Solutions** [solving overlapping labels](decision%20tree%20and%20random%20forest/dependent_labels.ipynb)
- only use unoverlapped data
- use a smaller bag of data
- separate the data into unoverlapped groups, train classifiers on each group separately and ensemble them together.

### Feature importance

One way of interpreting the model is by calculating how much each feature contributed to the model prediction, which is called feature importance. By studying feature importance we can figure out which feature is important for the prediction and which feature is not. Then we can abandon those irrelevant features and focus our energy on those significant features. By doing this we can enhance our model's performance. There are many wawys to calculate feature importance and the current state of the art is the shapley additive explanation. The feature importance in sklearn is calculated by the weighted difference of the gini impurity of the parent node and the gini impurity of the left and right child nodes on which the feature split. And the weights are given by the number of data points in each node. but this way of computing feature importance is inconsistent since it gives more importance to features used to split nodes far away from the root, which motivates the use of current feature attribution method -- Shapley Additive Explanations. The method comes from coalition game theory. The idea of this method is to calculate the feature importance by seeing how well the model perform with and without the feature for every data point. So this method calculates the feature importance for each individual data point(the local feature importance). We can calculate the global feature importance by aggregating each local feature importance.

[The notebook of calculating Shapley values](decision%20tree%20and%20random%20forest/calculate_shap.ipynb)

[Implement the simple version of the Tree Shap algorithm to train and reuse a single tree model based onScott Lundberg's paper Consistent Individualized Feature Attribution for Tree Ensembles](decision%20tree%20and%20random%20forest/tree_shap.ipynb)


## Backtesting
A backtesing is said to be valid if it satisfies at least 1)the profit calculation is realistic, i.e., the simulated profit and loss can actually be acheived by trading the same instruments the same way the backtest code indicated. 2) the startegy constructed does not benefit from look ahead bias or from hindsight.

### Time delay


### Transaction cost

For institutional traders, the transaction cost is due to the impact a trade has on the market price of the asset being bought or sold. 

#### Linear impact model

We assume that there is a linear relation between the transaction size(percentage of the average daily volume) and the percent change in price, and we assume that 1% of average daily volume traded will result in 10 basis point (10/10000 = 0.1%) change in price, i.e., we have 

 % change in price/ trade size = 10 basis point/ 1% of average daily volume 

 We can deduce that 
 transaction cost = \sum \lambda_i(h_{i,t}-h_{i,t-1}) where h_{i,t} is the holding of stock i at time t.

 #### Square root model
 [Crossover from Linear to Square-Root Market Impact](https://arxiv.org/pdf/1811.05230.pdf)

 ### Optimization with transaction cost

 Define objective function and its gradient, input these into an optimizer.

 Optimizer to choose from:
 - L-BFGS: designed to more efficiently handle large scale problem
 - Powell
 - Nelder-Mead
 - Conjugate gradient

[Reference on the various optimizers that are available in scipy](http://scipy-lectures.org/advanced/mathematical_optimization/)

[Insightful explanation of various optimization algorithms](http://web.stanford.edu/class/ee364b/lectures.html)


### Interpretation of profit and loss of alpha(performance attribution)

### Portfolio optimization with transaction cost
[A notebook of portfolio optimization with transaction costs]

