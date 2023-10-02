# Backtesting

Build a realistic backtest using Barrad data which perform portfolio optimization by minimizing common risk, special risk, transaction cost and maximizing expected return.

Use performance attribution to identify the major drivers of the portfolio's PnL.

## Workflow
- load the preprocessed barrad data from pickle files: factor exposure in 2004; factor return covariance in 2003, 2004; daily return in 2004, 2005
- shift daily return data for 2 days: incorporate time dalay in live trading, use daily return data two days after the factor exposure data and factor return covariance data, merge the factor exposure and the 2 day delay daily return data into a dictionary called frames
- winsorizing: clip the daily return data by an upper bound and lower bound to help us reduce the infleence of outliers
- eatimate the factor return of each factor and each day: estimate the factor return using ordinary least square with factor exposures as independent variables and daily return as dependent variable, store them into a dictionary facret with date as key
- choose alpha factors and combine them into alpha vector $\alpha$ and compute the expected return $\alpha * h$ where $h$ is the portfolio holding: choose reversal, earning yields, values and sentiment as our alpha factors, plot the cultimate sum of expected factor return of the alpha factors in year 2004
- initialize the first holding: our initial holding would be one stock with largest market capitaliztion with zero holding
- build universe based on filter: our portfolio only include stocks with market capitalizaiton at least one billion dollars, if the stocks previously is included in our portfolio, we continue to include them even now their market cap is lower than one billion
- compute the matrix of risk factor exposures using 'patsy.dmatrices'
- compute the specific variance S and the idiosyncratic risk $h^tSh$
- compute the risk factor covariance matrix using the covariance data, in order to simplify multiplication, only take the diagonal of the matrix which contains the variance of the factor. We can do this since later in our portfolio optimization we will minimize the exposure of the portfolio to the risk factors as much as possible, thus it is less important to know whether the risk factors are correlated or not.
- compute the common risk which is $h^tBFB^th$ where $h$ is the portfolio holdings, $B$ is the factor exposure matrix, $F$ is the factor covariance matrix
- compute the transaction cost, which is the multiplicaiton of the price change due to market impact and the dollars traded:
- $$ cost = \sum_{i=1}^{N}\lambda_{i,t}(h_{i,t}-h_{i,t-1})^2$$ where $h_{i,t}$ is the holding dollars of stock i at time t and $\lambda_{i,t}=frac{1}{10 * ADV_{i,t}}$ where $ADV_{i,t}$ is the 30 days moving average of the average daily volume of stock i at time t.
- construct the objective function: minimizing the common risk(risk comes from common risk factors), special risk(risk comes from special variance, maximizing the expected return(return comes from the alpha factors), minimizing the transaction cost
- compute the gradient of the objective function
- perform portfolio optimization using 'scipy.optimize.fmin_l_bfgs_b(func = objective function, x0 = initial holding, fprime = gradient)'
- compute the profit and loss attribution: attribution to the alpha factors and risk factors are the products of the factor returns and factor exposure and the holding respectively
- build_portfolio_characteristics: calculate the sum of long positions, short positions, net positions, gross market value, and amount of dollars traded
