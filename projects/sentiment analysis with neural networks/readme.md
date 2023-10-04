# Sentiment Analysis With Neural Networks

> build a sentiment analysis model that will learn to assign sentiment to twits on social media site StockTwits on its own using labeled data.


## Workflow
- load the labeled twits from json file
- preprocess the data: using regular expression to remove ticker symbol, username, url, numbers, single characters that do not provide sentiment information, tokenize and lemmatize it
- build a recurrent neural network consists of embed layer, lstm layer, fully connected layer and softmax layer
- train and validate the neural network
- use the neural network for sentiment prediction of twits
- use the model to track the sentiments of various stocks by predicting the sentiments of twits as they are coming in
