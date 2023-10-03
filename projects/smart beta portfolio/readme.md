# Smart Beta Portfolio and Portfolio Optimization
[The notebook for the project.](project_3_starter.ipynb)

## Project Contents
> Smart beta ETFs can be designed by two general methods：alternative weighting and minimum volatility. In this project, we build two kinds of smart beta portfolios using these two kinds of methods. 
>
> We first build a smart beta ETF weighted by the dividends issuing situation of the company. The hypothesis is that dividends-issuing stocks tend to perform better than stocks that do not, since companies that issue dividends regularly might have better financial situation and act in the best interest of their shareholders.
>
> Then we build another portfolio weighted by realizing the goal of tracking the market capital index closely, while also minimizing the portfolio volatility. Finally, we rebalance the portfolio overtime and analyse the portfolio turnover.

## Project Workflow
1. select large dollar volume stocks, load and view their close prices and volume
2. construct a smart beta portfolio:
   - compute the index weights based on dollar volume traded on that day
   - compute the portfolio weights based on total dividend yield over time
   - generate the return data for all the stocks and dates
   - compute the weighted returns for the index and the smart beta ETF
   - compute the cumulative returns for the index and the ETF and compare them
   - evaluate the performance of the smart beta portfolio by computing the annualized tracking error between the ETF and the benchmark index
3. build a smart beta portfolio which tracks the index closely and minimizing the portfolio variance using convex optimization
   - compute the covariance matrix of the return of each stocks
   - compute the portfolio variance
   - construct the objective function and the constraints
   - perform convex optimization to get the weights of the portfolio
   - analyse the performance of the portfolio by comparing its return with the index returns
   - rebalance the portfolio every 5 days
   - compute the turnover for the rebalancing

