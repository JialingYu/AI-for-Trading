# Neural Network
## Notebooks

- [a notebook for gradient descend](notebooks/GradientDescent.ipynb)
## Introduction to neural network
### Cost function(Loss function)
In optimization, the objective function is usually to minimize the loss function, which is usually a globally differential function.  
There are mostly two kinds of cost function, the square loss function, which  measures the square of the distance between the measurement and the goal; and the absolute loss function, which measures the absolute distance between the measurement and the goal.

One way to minimize the cost funcition is by **gradient descend**, which moves the point to the opposite direction of the gradient of the cost function, i.e., move the point along with the direction that the value of the cost function descends the most.  
The gradient of the cost function at some point is a vector whose direction is the direction that the fucntion ascends the fastest at that point, and the magnitude is the amount of ascendent.

### Entropy
In information theory, entropy of a random variable X describes the level of information or uncertainty of the outcome of the random variable. The more uncertain the outcome is, the higher the entropy. For example, flipping a fair coin has less entropy than rolling a fair dice. Since flipping the coin has only two possible outcomes, of which each has probability 1/2, while rolling a dice has 6 possible outcome, of which each has probability 1/6. In addition, flipping an unfair coin which 4/5 probability with head and 1/5 probability with tail has lower entropy than flipping a fair coin, since the former situation is more certain.

The entropy of a discrete random variable X with probability distribution $p(x)$ is 
$$H(X)=\sum p(x)log_a(1/p(x))=E(-log(p(x)))$$
where a is the base of the logarithm.

### Cross Entropy
The cross entropy of a discrete distribution q relative to a distribution p is 
$$H(p,q)=-\sum p(x)log q(x)=E_p(-log q(x))$$

### Artificial Neural network
There are two kinds of artificial neural network: feedforward neural network and recurrent neural network, charactered by the direction of flow of information between layers. The feed forward neural network is a unidirection neural work, meaning that information transfer from one layer to the next layer in order, with no cycle. And recurrent neural network is a bidirectional neural network, which means it allows output from a specific node to affect the input of the same node.

Feed forward neural network is usually trained by back propagation, which is, we first feed the model with labeled data with some randomly initialized weights, and get the output; and then we measure the distance between the disired label and the output by cost function and try to minimize the cost function by adjusting the weights.

The main idea of neural network is to combine different liear models to get a non linear model. 

A linear model is a continuous **perceptron** with input $x_1,\dots,x_n$, weights $w_1,\dots, w_n$ and bias $b$, and output $\sigma(w_1x_1+\dots+w_nx_n+b)$ where $\sigma$ is the sigmoid function $\sigma(x)=\frac{1}{1+e^{-x}}$.

#### Activation function
##### logistic function
Logistic function is defined as
$$f(x)=\frac{L}{1+e^{-k(x-x_0)}}$$
where $x_0$ is the $x$ value of the function's midpoint, $L$ is the supremum of $f(x)$ and $k$ is the steepness of the curve.
The sigmoid function is the standard logistic funtion where $L=1$, $x_0=0$, $k=1$:
$$\sigma(x)=\frac{1}{1+e^{-x}}$$.

When the output of the neural network has one outcome, we can use the logistic funciton as the activation function. We can apply the sigmoid function to the output and turn it into a probability distribution, i.e., a value between 0 and 1. 

##### softmax function
The softmax function is a generalization of the logistic function to multi-dimension. The function takes a vector $(x_1, \dots,x_n)$ as input and output a $n$ dimensional vector of values between 0 and 1 and proportional to the exponentiation of the input values:
$$\sigma: \mathbb{R}^{n}\to (0,1)^{n}$$
$$\sigma(x_i)=e^{x_i}/\sum^{n}_{i=1}e^{x_i}$$

When the neural network has more than 1 outcome, we can apply the softmax function as the activation function and turn the outcome into the probability distribution.

##### Hyperbolic tangent function and the rectified linear unit(relu)
Since the slope of the sigmoid function becomes very small when the variable is big or small enough, this makes gradient descent difficult when the derivative is so small. To solve this, we can choose other activation function such as the hyperbolic tangent function and the rectified linear unit(relu).

The hyperbolic tangent function is defined as
$$tanh(x)=\frac{e^x-e^{-x}}{e^x+e^{-x}}$$
which ranges between -1 and 1.

The relu function is defined as $relu(x)=x$ when $x\geq 0$ and $relu(x)=0$ when $x<0$.

### Neural network architecture
-feed forward: feed the data into multilayer perceptrons(multi layer linear model)
-back propagation: minimize the cost function using gradient descent to adjust the weights of each perceptron

Here is [a notebook using neural network to predict student's admission to graduate school](notebooks/StudentAdmissions.ipynb)

#### training the neural network
To prevent underfitting and overfitting, we can use the early stop algorithm to train the neural network, i.e., we stop the training when the testing error stop decreasing and start to increase.


## Deep learning with pytorch
[A notebook of building a simple neural network in pytorch.](notebooks/IntroductiontoDeepLearningwithPyTorch.ipynb)

[A notebook of using pytorch to build a neural network architechure to train the MNIST data](notebooks/NeuralnetworkswithPyTorch.ipynb)

[A notebook of training the neural network using pytorch](notebooks/TrainingNeuralNetworks.ipynb)

[A notebook of building and training a neural nework for fashion.mnist data set](notebooks/Fashion-MNIST.ipynb)

[A notebook of inference and validation of the trained neural network and solving overfitting using dropout]

[A notebook of saving and loading model with pytorch](notebooks/Part6-SavingandLoadingModels.ipynb)

## Recurrent Neural network
Different from traditional feedforward neural network(NN), which information only goes in one direction, reccurent neural network(RNN) has a loop which allows information to preceed so that we can use past information for present task. However, it turns out that standard reccurent neural network is only able to use the recent past information, i.e., it is only able to remember short term information. To address this isseue, we use a special kind of reccurent neural network--LSTM(long short term memory) network.

[A notebook of building and training a character-level LSTM in PyTorch and using it for prediction](notebooks/Character_Level_RNN.ipynb)


## Word Embeddings and word2vec

**Word embedding** is a representation of a word using vector of real numbers(i.e., a mapping from words to vectors) which encodes the meaning of the words so that words that are closer in vector space has similar meanings.

Methods to generate the mapping include neural networks, dimension reduction, etc. Word embedding used as representation of inputs can boost the performance in NLP tasks like sentiment analysis.

**Word2vec** is a group of models to produce word embedding. It uses a shallow, two layers neural network to learn the word association of a large corpus of texts. It takes the corpus as an input and produces a several hundred dimensional vector space with each unique word in the corpus associated with a vector in the vector space. The vectors are chosen carefully so that they reflect semantic and syntactic qualities of words. Thus we can use a simple math function such as cosine similarity to detect the level of semantic similarity of words.

There are two architecture to produce the vectors: **continuously sliding bag-of-words(CBOW)** and **continuously sliding skip-gram**. In both architecture, word2vec considers both the word itself and a sliding context window as it iterates over the corpus.

[A notebook of using PyTorch to implement the Word2Vec algorithm using the skip-gram architecture](notebooks/NegativeSamplingExercise.ipynb)

Workflow for the notebook:
- load the data
- preprocess the data: convert the data into a list of tokens; create two dictionaries to convert words to integers and back again; subsampling the data
- making batches: return batches of input and target data for our model, where the input is a word of the text and the target is the surrounding context over a window surrounding that word
- create the SkipGram model
- train and validate the model
- improve the training efficiency of the model using negative sampling


## Sentiment Prediction RNN

[A notebook using RNN to perform sentiment analysis on movie comments](notebooks/Sentiment_RNN_Exercise.ipynb)

**Workflow of the notebook:**

- load in and visualize the data: load in the reviews file and the labels file
- data preprocessing:
    - lower the letters and remove punctuations; split the review strings into a list of reviews using separator '\n'; split the reviews into a list of words
    - encode the words: create a dictionary map words to integers using `collections.Counter()`; convert the list of reviews into a list of lists of integers.
    - encode the labels: convert the labels into a list of zeros and ones
    - remove outliers: remove reviews has length 0, pad short reviews with 0 on the left and truncate long reviews; create a numpy array to store padded data in a standard shape
    - create training, validation and test sets
    - create data loader and batch the data sets
- create the sentiment network with pytorch
    - build the embedding layer
    - build the LSTM layer
    - build the fully connected layer to map the data into the desire output_size
    - build the sigmoid activation layer turning all output into value between 0 and 1
- instantiate, train, validate, test the network
- inference on the network using  unseen positive and negative test review
