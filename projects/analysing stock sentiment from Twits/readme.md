# Analysing Stock Sentiment From Twits

> This project build a sentiment analysis model which assigns 5 sentiments(extremly positive, positive, neutral, negative, extremly negative) to twits from the social media site StockTwits using labeled data.


## Workflow
-load Twits data: load the json file of 1548010 labeled twits.
- preprocess the data:
    - remove ticker symbol, username, url since they do not provide sentiment;
    - tokenize and lemmatize the data
    - create a bag of words of our data and a dictionary counting the words
    - remove too often and too rare words from our data
    - balance the classes of our data so that each sentiment shows up as frequently in our data
    - convert tokens into integers so that we can pass to the neural network.
      
