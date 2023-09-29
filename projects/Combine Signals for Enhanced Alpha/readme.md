# Combine Signals for Enhanced Alpha

Data: end of day from Quotemedia and sector data from Sharadar

## Workflow
- build the data pipeline and get the returns
- add three alpha factors to the data pipeline, add the quant, regime, sector, date features to the pipeline
- get the 5 days trailing returns as the target, and check the i.i.d of the target
- split the data into train, valid, test sets, train random forests using different tree sizes and analyse the sharpe ratios, factor rank autocorrelation.
- address the overlapping samples problems using three methods, train different sizes random forests on them separately, and analyse the sharpe ratios, factor rank autocorrelation.
