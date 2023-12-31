# Natural Language Processing on Financial Statements

[The notebook for the project](project_5_starter.ipynb)

## Goal
> Perform NLP Analysis on 10-k financial statements to generate an alpha factor. For the dataset, we'll be using the end of day from Quotemedia and Loughran-McDonald sentiment word lists.

## Description
We will access the SCC website to get the 10-k filings and extract key sections for NLP analysis. We will use several python libraries to implement the analysis and create a text-based stock selection model. This stock selection model was originally described in the paper [Lazy Prices](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1658471), which investigates how changes in a particular section of the financial statements can be used for stocks picking.

## Workflow
- read 10-k reports from a csv file
- preprocess the data
- perform sentiment analysis on 10-ks and create alpha factors
- evaluate alpha factor


### Read 10-k reports from a csv file
- read the csv file of 10-k reports from the US Securities and Exchange Commission into a pandas dataframe; 
- get the text between the html label `<DOCUMENT>` and `</DOCUMENT>` using regular expression ;
- get the document type after the html label `<TYPE>` using regular expression `<TYPE>[^\n]+`;
- filter out non 10-k documents


### Preprocess the data
- clean up the text: remove the html labels using `BeautifulSoup`; lowercase the text
- lemmatization: lemmatize the verbs of the text using `WordNetLemmatizer().lemmatize(w, pos='v')`
- remove stopwords



### Perform sentiment analysis on 10-ks and create alpha factors
- load and process the Loughran McDonald Sentiment Word Lists
- generate sentiment bag of words of documents: using the word list, generate a sentiment bag of words of all 10-ks using `sklearn.feature_extraction.text.CountVectorizer`, i.e., generate a 2d numpy array of which first dimension is the documents and the second dimension is the words of a particular sentiment from the word list.
- compute the Jaccard Similarity of the bag of words:  compute the Jaccard Similarity between the succesive 10-ks for every sentiment and every ticker using `sklearn.metrics.jaccard_similarity_score`, i.e., compute the Jaccard Similarity of two neighbouring rows of the 2d numpy array bag of words.
-  generate sentiment TFIDF from the 10-k documents using `sklearn.feature_extraction.text.TfidfVectorizer`
-  get cosine similarities for each neighboring TFIDF vector/document

### Evaluate alpha factors
We take the cosine similarities of every sentiments as our alpha factors and evaluate them. This evaluation can also be applied to the Jaccard Similarity as well.

- get price data: get the yearly closing price data to run the factor against
- convert the cosine_similarities dictionary into dataframe for alphalens to use
- turn the factor data, price data into data suitably formatted for alphalens using `alphalens.utils.get_clean_factor_and_forward_returns`
- get the factor return using `alphalens.performance.factor_returns`
- Basis Points Per Day per Quantile: compute the quantile return of the alpha factor using `alphalens.performance.mean_return_by_quantile()`. a good alpha factor should be monotonic in quantiles
- turnover analysis: measure how stable an alpha factor is by Factor Rank Autocorrelation using `alphalens.performance.factor_rank_autocorrelation()`
- compute the sharpe ratio of the alpha factor of each sentiment

