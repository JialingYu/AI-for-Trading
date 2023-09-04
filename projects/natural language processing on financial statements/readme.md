# Natural Language Processing on Financial Statements

## Goal
> Perform NLP Analysis on 10-k financial statements to generate an alpha factor. For the dataset, we'll be using the end of day from Quotemedia and Loughran-McDonald sentiment word lists.

## DEscription
We will access the SCC website to get the 10-k filings and extract key sections for NLP analysis. We will use several python libraries to implement the analysis and create a text-based stock selection model. This stock selection model was originally described in the paper [Lazy Prices](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1658471), which investigates how changes in a particular section of the financial statements can be used for stocks picking.

## Workflow
- collect 10+k reports from the US Securities and Exchange Commission
