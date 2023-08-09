# Multifactor model
## main strategy
> create a alpha model and a risk model, and then use them to create a portfolio which trades as close as to the alpha model while limiting risk as measured by the risk model
### workflow
1. create a risk model
2. create a alpha model
3. create a portfolio using alpha model and risk model



### create alpha factors

We create the following alpha factors
- Momentum 1 Year Factor
- Mean Reversion 5 Day Sector Neutral Factor
- Mean Reversion 5 Day Sector Neutral Smoothed Factor
- Overnight Sentiment Factor
- Overnight Sentiment Smoothed Factor

#### momentum 1 year factor
hypothesis: higer past 1 year(252 days) return are proportional to future return
use `zipline.pipeline.factors.Returns`

#### Mean Reversion 5 Day Sector Neutral Factor
hypothesis: Short-term outperformers(underperformers) compared to their sector will revert

use `zipline.pipeline.factors.Returns`

#### Mean Reversion 5 Day Sector Neutral Smoothed Factor
smooth the above using `zipline.pipeline.factors.SimpleMovingAverage`

#### Overnight Sentiment Factor
hypothesis: stocks with high (low) overnight returns underperform (outperform) over the longer-term
from the paper: [Overnight Returns and Firm-Specific Investor Sentiment](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2554010)
use data `zipline.pipeline.data.USEquityPricing`

#### Overnight Sentiment Smoothed Factor
smooth the above factor using `zipline.pipeline.factors.SimpleMovingAverage`
