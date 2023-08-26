# Smart Beta Portfolio and Portfolio Optimization
[The notebook for the project.](project_3_starter.ipynb)

## Project Contents
> We first build a smart beta ETF depending on the dividends issuing situation of the company. The hypothesis is that dividends-issuing stocks tend to perform better than stocks that do not, since companies that issue dividends regularly might have better financial situation and act in the best interest of their shareholders. Then we optimize the portfolio by minimizing its variance and its difference from the market capital weighted index. Finally, we rebalance the portfolio overtime and analyse the portfolio turnover.

## Project Workflow
1. select large dollar volume stocks, load and view their close prices and volume
2. construct a smart beta portfolio:
   - compute the index weights based on dollar volume traded on that day
   - compute the portfolio weights based on total dividend yield over time
   - generate the return data for all the stocks and dates
   - compute the weighted returns for the index and the smart beta ETF
   - compute the cumulative returns for the index and the ETF and compare them
3. evaluate the performance of the smart beta portfolio by computing the annualized tracking error between the ETF and the benchmark index
4. optimize the smart beta portfolio

