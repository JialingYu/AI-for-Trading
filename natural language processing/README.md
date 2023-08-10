
# Natural Language Processing

**why use it?**

Unlike math and computer language which is structured, human language are ambiguious and unstructured, which makes computer difficult to understand.  
Despite that, computer can still do something to understand unstructured human language such as the following:
- process words and phrases, try to identify keywords, part of speech, name entities, quantities, etc.
- parse sentence to extract relevant parts of sentence, questions, statements
- analyse document vto find frequent and rare words, assess tone and sentiment, cluster and group relevant documents together.

## NLP pipeline
1. text processing: take raw input text, clean and normalize it, convert it into a form that suitable for feature extraction
2. features extraction: extract and produce features which are appropriate for the type of model you are going to use
3. modeling: build statistical or machine learing model, train the model with data using optimization, predict unseen data using the model

### 1. Text processing 
[A notebook for text processing tweets](notebooks/process_tweets.ipynb)

[A notebook for text processing](notebooks/text_processing.ipynb)

convert natural language sentence into a sequence of normalized words

The typical work flow:
- capture text data: convert different sources of data into plain text
- normalization: start with a plain text sentence, normalize it by converting to lower case and removing puntuations
- tokenization: split the sentence into words(tokens) using a tokenizer
- stop words removal: remove stop word to reduce the vocabulary you have to deal with
- stemming and lemmatization: apply lemmatization and stemming to reduce the words to the stem form

#### 1.1. Capture text data
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

#### 1.2. Text normalization
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

#### 1.3. Tokenization
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

#### 1.4. Stop words removal
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

We can use the `nltk.tag.pos_tag(tokens)` function to tag a given list of tokens. The function return a list of tuples of each word and its tag.
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

- Part of speech tagging can be used to parse sentence.  
- For more about tagging, one can refer to the [nltk book](https://www.nltk.org/book/ch05.html).

#### Named entity recognition
A named entity is a real world object such as a person, organization, that can be represented by a name. Named-entity recognition is a subtask of information extraction that aims to locate and classify named entities in an unstructured text into predefined categories like person, organizations.    
After perform part of speech tagging on a list of tokens, we get a list of POS-tagged tokens. We can then perform named entity recognition on the list using `nltk.ne_chunk()` function. This function takes a list of POS-tagged tokens as inputs and return a tree of named entity.

```python
from nltk import pos_tag, ne_chunk
from nltk.tokenize import word_tokenize
#word tokenize the sentence, and then tag parts of speech, and then identify named-entity
ne_chunk(pos_tag(word_tokenize('Jialing is studying Udacity nano degree program in Sweden')))
```

Named entity recogniztion can be used to search for new articles on campanys of interest.

#### 1.5. Lemmatization and stemming
Natural lanugage use different forms of words but with similar meaning for grammatical reasons, e.g, is, was, are. Stemming and Lemmatization have similar goal, which is to reduce the different forms of words into its stem. For example, reduce is, are, was to be. The difference is that stemming just cut off the end of the words and do not use context, while lemmatization use a dictionary to perform the task and reduce the words according to their surrounding context. For example, for the word 'see', stemming would reduce it into 's' while lemmatization would reduce it into 'see' or 'saw' depending on whether the use of the token is a verb or a noun. Since stemming do not require a dictionary, it is usually easier to implement and run faster.

**stemming**
nltk has a few different stemmer [nltk stemmer](https://www.nltk.org/api/nltk.stem.html) including the follwing `PorterStemmer` class.
```python
from nltk.stem.porter import PorterStemmer
#reduce words to their stem
words=['was','is','goes']
stemmed = [PorterStemmer().stem(w) for w in words]
print(stemmed)
```

**lemmatization**
NLTK by default use the `WordNetLemmatizer` class, which lemmatize using WordNet's built-in morphy function. Return the input word unchanged if it cannot be found in WorldNet. A Lemmatizer by default need to know the part of speech for each word it is trying to transform, which can be specified by the pos parameter. By default pos = 'n' which stands for noun.
```python
from nltk.stem.wordnet import WordNetLemmatizer
#reduce words to their stem
words=['was','is','goes']
stemmed = [WordNetLemmatizer().lemmatize(w, pos = 'v') for w in words]
print(stemmed)
```
Here is [a webpage for more about  stemming and lemmatization.](https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html)





### 2. Feature Extraction
2.1. bag of words
2.2. TF-IDF
2.3. one hot encoding
2.4. word embedding
2.5. Word2Vec
2.6. GloVe
2.7. embedding for deep learning
2.8. t-SNE


### 3. Use NLP to extract financial info from 10-Ks

For long term investment, we need to read financial reports such as 10-k reports from SEC(u.s. security and exchange commissions) for company information. The EDGAR database of SEC contains all financial reports. We can visit [the website of SEC](https://www.sec.gov/) to visit the EDGAR database, and then search each company by its ticker symbol, e.g., AAPL for apple. 

#### use regex to process .txt file
One way to extract data from 10-K reports is to use regular expression to process the `.txt` file of the 10-K reports. If the 10-K report is in HTML format, we can first transform it into txt format, and then process it.

In the following we will show how to create regular expression using python.    
Regular expression(regex, regexp) is a sequence of characters that specify a match pattern in text. Such patterns are used by string-searching-algorithm for "find" or “find and replace” operation on strings.

##### Regular expression can be used to match letters and metacharacters:

In order to find words using regular expression in a text, we first create a regular expression object from raw string using `compile()` fucntion from the python `re` module, and then use the `finditer()` object method to find the iterations of the regular expression. The function returns an iterator object which we can iterate through.

We need to use raw string to create regular expression since regular expression escape special characters(meta characters) just as string, thus we need to use raw string(backlash '\' would not be used to escape) to avoid conflict. [notebooks for raw strings](notebooks/raw_strings.ipynb)

Here is a notebook of basic workflow of [creating regular expression to find words](notebooks/finding_words.ipynb)

Meta characters specify special meaning and can not be searched directly. We need to use backslash to escape them first.
Here is a [notebook for meta characters](notebooks/finding_metacharacters.ipynb)

##### Regular expression can be used to match more complicated pattern:
- We have seen before that backlash can be used to escape all metacharacters. It can also be followed by some different characters to signal different special sequences. For example, `\d` signals digital characters, `\D` signals non digital characters, `\s` signals whitespace character, `\S' signals non whitespace  characters, etc.

Here is a [notebook searching for simple patterns](notebooks/simple_patterns.ipynb).

- We can use the special expression `\b` to indicate word boundary. A word in this case is a sequence of alphanumeric characters(0-9, a-z, A-Z, _) while a word boundary are white space, non alphanumeric characters or the beginning or ending of a string. 

Here is a [notebook for word boundary.](notebooks/word_boundaries.ipynb)

- Regular expressions use metacharacters to give special instruction. Regular expression use the following metacharacters `. ^ $ \ ？ * [ ] { } ( ) |`.    
The dot `.` matches any characters except new line `\n`    
The caret `^` matches the characters only when they appear at the beginning of the string    
The dollar sign `$` matches the characters only when they appear at the end of the string    
`[]` indicates a set of characters, one character within the set is matched, e.g., `[a-z]` matches one lower character. Special characters within a set have no special meaning anymore, and the character  itself is matched.
`|` is used in a set indicates 'or', e.g., `[a|b]` matches a or b
`(...)` indicates the start and end of a group and matches whatever regular expression within the group. After matched, each group can be retrieved within a string using `\number`
`{m}` matches the preceeding character m times    
`{m,n}` matches the preceeding character at least m times at most n times    
`?` matches the preceeding character 0 or 1 time, i.e., the preceeding character is optional  
`*` matches the preceeding character 0 or more times    
`+` matches the preceeding character 1 or more times.

Here is a [notebook for simple_metacharacters.](notebooks/simple_metacharacters.ipynb)

Here is a [notebook for character_sets](notebooks/character_sets.ipynb)

Here is a [notebook for finding_complicated_patterns](notebooks/finding_complicated_patterns.ipynb)

- The regular expression object `regex` has a method `sub(raw_string, sample_text)` which can be used to substitute every match of regular expression in the sample_text by raw string.

  Here is a [notebook for substitution.](notebooks/substitutions_and_flags.ipynb)
  
  Here is a [python regular expression document.](https://docs.python.org/2/library/re.html#module-re)

  Here is a [notebook of using regular expression to extract item 1A, 7 and 7A from 10-K reports: ](notebooks/applying_regexes_10ks.ipynb)

As we can see from above notebook, using regular expression to process txt file and extract info from scratch is difficult. Luckily we have the `beautifulsoup` library which can be used to directly process HTML website.

#### use `beautifulsoup` to process 10-Ks in HTML or XML format.
  
  
  

















***The following is just markdown syntax for myself to remember***
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


