
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

### 1. text processing: convert natural language sentence into a sequence of normalized tokens

The typical work flow:
- capture text data: convert different sources of data into plain text
- normalization: start with a plain text sentence, normalize it by converting to lower case and removing puntuations
- tokenization: split the sentence into words using a tokenizer
- remove stop word to reduce the vocabulary you have to deal with
- apply lemmatization and stemming to reduce the words to the stem form

#### capture text data
Typical source of data including 
- .txt file(plain text): os library: can be read using python built in file input mechanism
```python
{
  import os

  with open ("sample.txt", r) as f:
    text = f.read()
    print(text)
}
```
- .csv file(Tabular data): 
```python
{
  import pandas as pd

  #read the tabular csv file into dataframe
  df = pd.read_csv("sample.csv")
}
```
- online resourse: requests library: requests.get()
```python
{
  import requests

  #get data from an API
  text = requests.get(API url)
  res = text.json()
}
```

#### text normalization
- convert all letters into lower case
```python
{
  #use string method lower() to lower the text
  text = text.lower()
}
```
- remove punctuation:
  
```python
{
  import re

  #substitute punctuations with blank space
  text = re.sub(r'[^a-zA-Z0-9]', ' ', text)
}
```



















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


