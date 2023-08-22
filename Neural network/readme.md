# Neural Network
## Notebooks

- [a notebook for gradient descend](notebooks/GradientDescent.ipynb)

## Cost function(Loss function)
In optimization, the objective function is usually to minimize the loss function, which is usually a globally differential function.  
There are mostly two kinds of cost function, the square loss function, which  measures the square of the distance between the measurement and the goal; and the absolute loss function, which measures the absolute distance between the measurement and the goal.

One way to minimize the cost funcition is by **gradient descend**, which moves the point to the opposite direction of the gradient of the cost function, i.e., move the point along with the direction that the value of the cost function descends the most.  
The gradient of the cost function at some point is a vector whose direction is the direction that the fucntion ascends the fastest at that point, and the magnitude is the amount of ascendent.

## Entropy
In information theory, entropy of a random variable X describes the level of information or uncertainty of the outcome of the random variable. The more uncertain the outcome is, the higher the entropy. For example, flipping a fair coin has less entropy than rolling a fair dice. Since flipping the coin has only two possible outcomes, of which each has probability 1/2, while rolling a dice has 6 possible outcome, of which each has probability 1/6. In addition, flipping an unfair coin which 4/5 probability with head and 1/5 probability with tail has lower entropy than flipping a fair coin, since the former situation is more certain.

The entropy of a discrete random variable X with probability distribution $p(x)$ is 
$$H(X)=\sum p(x)log_a(1/p(x))=E(-log(p(x)))$$
where a is the base of the logarithm.

## Cross Entropy
The cross entropy of a discrete distribution q relative to a distribution p is 
$$H(p,q)=-\sum p(x)log q(x)=E_p(-log q(x))$$

## Neural network
The main idea of neural network is to combine different liear models to get a non linear model. 

A linear model is a continuous **perceptron** with input $x_1,\dots,x_n$, weights $w_1,\dots, w_n$ and bias $b$, and output $\sigma(w_1x_1+\dots+w_nx_n+b)$ where $\sigma$ is the sigmoid function $\sigma(x)=\frac{1}{1+e^{-x}}$.

### Activation function
#### logistic function
Logistic function is defined as
$$f(x)=\frac{L}{1+e^{-k(x-x_0)}}$$
where $x_0$ is the $x$ value of the function's midpoint, $L$ is the supremum of $f(x)$ and $k$ is the steepness of the curve.
The sigmoid function is the standard logistic funtion where $L=1$, $x_0=0$, $k=1$:
$$\sigma(x)=\frac{1}{1+e^{-x}}$$.

When the output of the neural network has one outcome, we can use the logistic funciton as the activation function. We can apply the sigmoid function to the output and turn it into a probability distribution, i.e., a value between 0 and 1. 

#### softmax function
The softmax function is a generalization of the logistic function to multi-dimension. The function takes a vector $(x_1, \dots,x_n)$ as input and output a $n$ dimensional vector of values between 0 and 1 and proportional to the exponentiation of the input values:
$$\sigma: \mathbb{R}^{n}\to (0,1)^{n}$$
$$\sigma(x_i)=e^{x_i}/\sum^{n}_{i=1}e^{x_i}$$

When the neural network has more than 1 outcome, we can apply the softmax function as the activation function and turn the outcome into the probability distribution.

## Neural network architecture
-feed forward: feed the data into multilayer perceptrons(multi layer linear model)
-back propagation: minimize the cost function using gradient descent to adjust the weights of each perceptron

Here is [a notebook using neural network to predict student's admission to graduate school](notebooks/StudentAdmissions.ipynb)

### training the neural network
To prevent underfitting and overfitting, we can use the early stop algorithm to train the neural network, i.e., we stop the training when the testing error stop decreasing and start to increase.
