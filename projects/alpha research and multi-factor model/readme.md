# Multi-factor Model
Here is the [project notebook.](project_4_starter.ipynb)

## Main idea
> create an alpha model and a risk model, and use them to construct a portfolio which trades as close as to the alpha model while limiting risk measured by the risk model

### Workflow
1. create data bundle
2. create a risk model to predict portfolio risk
3. create a alpha model using 5 different alpha factors
4. evaluate the alpha model
5. create a portfolio using alpha model and risk model


### 1. Date bundle
- data registration: we use `zipline` to handle our data. We created an end of day data bundle and register it in zipline.
- build a pipeline engine: We build a pipeline engine and use the `zipline.pipeline` package to acess our data.

### 2. Create a risk model

predict the portfolio risk using the formula $\sqrt{X^{T}(BFB^{T}+S)X}$ where
- X is the portfolio weights
- B is the factor betas
- F is the factor covariance matrix
- S is the  idiosyncratic variance matrix

### 3. Create alpha model

We create the following alpha factors and then combine theem into a single alpha model.
- Momentum 1 Year Factor
- Mean Reversion 5 Day Sector Neutral Factor
- Mean Reversion 5 Day Sector Neutral Smoothed Factor
- Overnight Sentiment Factor
- Overnight Sentiment Smoothed Factor

#### Momentum 1 Year Factor
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

### 4. Evaluate alpha factors
- Quantile analysis: a good alpha factor should be monotonic in quantile
- Turnoutover analysis: since trading costs, a good alpha should be stable, i.e, the alpha factor should not change much from period to period. We can measure this by [alphalens.performance.factor_rank_autocorrelation](https://quantopian.github.io/alphalens/alphalens.html?highlight=factor_rank_autocorrelation#alphalens.performance.factor_rank_autocorrelation)
- Sharp ratio: calculate the sharp ratio of the factor return which is the mean of the return divided by the standard deviation of the return times the anualized factor.


### 5. Create portfolio using alpha model and risk model
We create a portfolio which trades as close as to the alpha model while limiting risk as measured by the risk model.

use `CVXPY` python library for convex optimization.

*onjective function:* 
- maximize $\alpha^{T}*x + \lambda||x||_{2}$ where $x$ is the portfolio weight, $\alpha$ is the alpha factor, and $\lambda$ is a regularization parameter. 

*constraints:*
- predicted risk be less than some maximum limit
- maximum and minimum portfolio factor exposures
- market neutral constraint: the sum of the weights must be zero 
- leverage constraint: the sum of the absolute value of the weights must be less than or equal to 1.0
- minimum and maximum limits on individual holdings.
