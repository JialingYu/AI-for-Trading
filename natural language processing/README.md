
# Natural Language Processing

**why use it?**

Unlike math and computer language which is structured, human language are ambiguious and unstructured, which makes computer difficult to understand.  
Despite that, computer can still do something to understand unstructured human language such as the following:
- process words and phrases, try to identify keywords, part of speech, name entities, quantities, etc.
- parse sentence to extract relevant parts of sentence, questions, statements
- analyse document vto find frequent and rare words, assess tone and sentiment, cluster and group relevant documents together.

## NlP pipeline
1. text processing: take raw input text, clean and normalize it, convert it into a form that suitable for feature extraction
2. features extraction: extract and produce features which are appropriate for the type of model you are going to use
3. modeling: build statistical or machine learing model, train the model with data using optimization, predict unseen data using the model

### 1. text processing

convert natural language sentence into a sequence of normalized words

The typical work flow:
- capture text data: convert different sources of data into plain text
- normalization: start with a plain text sentence, normalize it by converting to lower case and removing puntuations
- tokenization: split the sentence into words(tokens) using a tokenizer
- stop words removal: remove stop word to reduce the vocabulary you have to deal with
- apply lemmatization and stemming to reduce the words to the stem form

#### 1.1. capture text data
Typical source of data including 
- .txt file(plain text): os library: can be read using python built in file input mechanism
```python
import os

#Read in a plain text file
with open(os.path.join("data", "hieroglyph.txt"), "r") as f:
    text = f.read()
    print(text)
```
- .csv file(Tabular data): 
```python
import pandas as pd

#read the tabular csv file into dataframe
df = pd.read_csv("sample.csv")
```
- online resourse: requests library: requests.get()
```python
import requests

#get data from an API
text = requests.get(API url)
res = text.json()
```

#### 1.2. text normalization
- convert all letters into lower case:
```python
#use string method lower() to lower the text
text = text.lower()
```
- remove punctuation:
  
```python
import re

#substitute punctuations with blank space
text = re.sub(r'[^a-zA-Z0-9]', ' ', text)
```

#### 1.3. tokenization
##### words tokenization
We can split the sentence into words using string method split():

```python
#split the string by blank space using string method split
words =  text.split()
```

We can also use the word_tokenize() function from the NLTK(natural language toolkit) library:

```python
from nltk.tokenize import word_tokenize

#split text string into a list of words
words = word_tokenize(text)
```
##### sentence tokenization
We can split the text string into list of sentences using sent_tokenize() function:

```python
from nltk.tokenize import sent_tokenize

#split text string into a list of sentences
sents = sent_tokenize(text)
```

[The NLTK.tokenize package](https://www.nltk.org/api/nltk.tokenize.html)

*A Jupternotebook for scraping a webpage:*
https://github.com/udacity/AIND-NLP/blob/master/text_processing.ipynb

#### 1.4. stop words removal
Stop words are uninformative words that ocurrs frequently but do not provide much meaning. We want to remove them so that we can reduce the amount of words we have to deal with.

The words that nltk consider as stop words in English:
```python
from nltk.corpus import stopwords
print(stopwords.words('english'))
```
We can use list comprehension plus filtering condition to remove stop words from a list "words":
```python
words_removed = [for w in words if w not in stopwords.words('english')]
```

#### part-of-speech(PoS) tagging

Identifying how words are used in the sentence can help us better understand what is being said. 

We can use the nltk.tag.pos_tag(tokens) function to tag a given list of tokens. The function return a list of tuples of each word and its tag.
```python
import nltk
from nltk.tag import pos_tag
from nltk.tokenize import word_tokenize

nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
#tokenize the string
tokens = word_tokenize('I say something')
#tag the parts of speech
tags = pos_tag(tokens)
print(tags)
```

Part of speech tagging can be used to parse sentence.  
For more about tagging, one can refer to the [nltk book](https://www.nltk.org/book/ch05.html).


















| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

```python
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media


Def 1
: whateerr

Def 2
: haha


<dl>
  <dt>First Term</dt>
  <dd>This is the definition of the first term.</dd>
  <dt>Second Term</dt>
  <dd>This is one definition of the second term. </dd>
  <dd>This is another definition of the second term.</dd>
</dl>

~~The world is flat.~~ We now know that the world is round.

Gone camping! :tent: Be back soon.

That is so funny! :joy:


