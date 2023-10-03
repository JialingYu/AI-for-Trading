# Breakout Strategy Project
[Notebook for the project](project_2_starter.ipynb)

## Main Trading Strategy
>Long the stocks whose close price is higher than its highest close price over the past 50 days, and short the stocks whose close price is lower than the lowest close price over the past 50 days.

The hypothesis behind the strategy:
1. Stocks ocillate in a range whithout news or significant investor trading interest.
2. Traders seek to capitalize on this behaviour by selling stocks at the top of the range and buying stocks at the bottom of the range, which reinforces the existence of the range.
3. When the stock break out of range due to news release or pressure from large investor:
   - the liquidity traders seek to mitigate their losses by covering their position, and this magnify the move out of range.
   - the move out of range attract other investor who due to herd behaviour would build position strengthen the trend.
  
## Project Workflow
- get the high, low and close price of each ticker and date: 
- compute the highest high price, the lowest low price of each stock for each day over a past 50 days window
- compute the long and short signal using breakout strategy:
  generate a long signal(1) when the close price is higher than the 50-day highest price and generate a short signal(-1) when the close price is lower than the 50-day lowest price; do nothing(signal is 0) in other cases.
- filter out repeated long and short signals
- compute lookahead(5,10,20 days) price return and lookahead signal return
- test for significance:
  - plot the histogram of the signal return
  - perform K-S test to find the outliers: compare the distribution of the signal return of each stock and the normal distribution of the signal return of all stocks with the general mean and standard deviation using 'scipy.stats.kstest'.
  - get the outliers: get those stocks whose p value is smaller than the p value threshold and Ks value above the ks value threshold.


## Alpha research process
In oder to mitigate the overfitting our strategy to market noise, we need to form and validate hypothesis before we implement our hypothesis to code. The process of alpha research consists of:

1. observe and research
2. form hypothesis: What feature of markets or investor behaviour would lead to a persistent anomaly that my signal will try to use?
3. validate the hypothesis
4. code expression
5. test in sample
6. test out of sample

## Spotting outliers in signal return

If we buy and sell the stock randomly, in this case we are not able to make money and the return of our signal should be normally distributed with mean zero, since we have equal possibility to buy and sell the stock when the price goes up and down. Ideadly, if we have a profitable signal, the distribution of its return should look like a slightly right skewed normal distribution, with its mean slightly above zero. But if the distribution is a bit too good or just wierd, we should be skeptical. There might be due to outliers data. We need to find out where and when does the outliers lie and the root cause of the outliers. It can be due to a data error or a ligitimate movement of real event. We can check the new or crosscheck with other data source to find out the reason.
