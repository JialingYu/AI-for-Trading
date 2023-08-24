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
  
## project workflow
