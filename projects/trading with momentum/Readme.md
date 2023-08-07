# Trading with momentum project
## main trading strategy
> For each month-end observation period, rank the stocks by previous return, long the top performing stocks and short the bottom performing stocks.

## project workflow
1. **load market data:**

   load the daily closing prices of stocks in S&P 500
   
2. **resample the daily closing price into monthly closing price**
3. **compute log returns:**

   $R_t = \log_e P_t-\log_e P_{t-1}$ where $R_t$ is return at time $t$ and $P_t$ is closing price at time $t$
4. **compute previous log returns and look-ahead log returns**

   shift the log return dataframe by 1 and -1
5. **compute trading signal:**
   
   rank the stocks by previous log returns, set the 10 top performing stocks with value 1 (i.e., long) and the 10 bottom performing stocks with value -1(i.e., short), other stocks with value 0(i.e., do not trade them)
6. **compute portfolio return using trading signal and look-ahead log returns:**
   
   $portfolio-return = \frac{trading-signal * look-ahead-log-return}{number-of-trading-stocks}$

7. **compute the mean of the portfolio return**
8. **perform T-test on the mean of portfolio return**

   null hypothesis $H_0$: the mean of portfolio return from the signal is zero.

## conclusion
If we set the level of significant $\alpha = 0.05$, the computed p-value is 0.073359. Hence we can not reject the null hypothesis, which indicates the mean of the portfolio return of our signal is zero.
