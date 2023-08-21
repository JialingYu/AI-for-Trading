# Neural Network

## Cost function(Loss function)
In optimization, the objective function is usually to minimize the loss function, which is usually a globally differential function.  
There are mostly two kinds of cost function, the square loss function, which  measures the square of the distance between the measurement and the goal; and the absolute loss function, which measures the absolute distance between the measurement and the goal.

One way to minimize the cost funcition is by **gradient descend**, which moves the point to the opposite direction of the gradient of the cost function, i.e., move the point along with the direction that the value of the cost function descends the most.  
The gradient of the cost function at some point is a vector whose direction is the direction that the fucntion ascends the fastest at that point, and the magnitude is the amount of ascendent.
