# Week 5 Notes

## Cost Function and Backpropagation

### Cost Function
- L = total number of layers in the network
- s<sub>l</sub> = number of units (not counting bias unit) in layer l
- K = number of output units/classes
- Cost function for regularized logistic regression:<br />
  ![Cost Function 1](images/cost_function_1.png)
- Cost function for neural networks:<br />
  ![Cost Function 2](images/cost_function_2.png)
  - Additional nested summation that loops through the number of output nodes
  - For regularization, we must account for multiple theta matrices
    - The number of columns in our current theta matrix is equal to the number of nodes in our current layer (including the bias unit)
    - The number of rows in our current theta matrix is equal to the number of nodes in the next layer (excluding the bias unit)
### Backpropagation Algorithm
- "Backpropagation" is neural-network terminology for minizing our cost function, similar to what we were doing with gradient descent in logistic regression and linear regression:<br />
  ![Backpropagation Algorithm](images/backpropagation_algorithm_1.png)
- ![BackPropagation Algorithm](images/backpropagation_algorithm_2.png)
### Backpropagation Intuition
- ![Backpropagation Intuition 1](images/backpropagation_intuition_1.png)
- Recall that our derivative is the slope of a line tangent to the cost function, so the steeper the slope the more incorrect we are. Let us consider the following neural network below and see hwo we could calculate some &delta;<sub>j</sub><sup>(l)</sup>:<br />
  ![Backpropagation Intuition 2](images/backpropagation_intuition_2.png)

## Backpropagation in Practice

### Implementation Note: Unrolling Parameters
- ![Implementation Note: Unrolling Parameters](images/implementation_note_unrolling_parameters_1.png)
- To summarize<br />
  ![Implementation Note: Unrolling Parameters](images/implementation_note_unrolling_parameters_2.png)
### Gradient Checking
- ![Gradient Checking 1](images/gradient_checking_1.png)
### Random Initialization
- Initializing all theta weights to zero does not work with neural networks. When we backpropagate, all nodes will update to the same value repeatedly. Instead we can randomly initialize our weights for our &Theta; matrices using the following method:<br />
  ![Random Initialization 1](images/random_initialization_1.png)
- ![Random Initialization 2](images/random_initialization_2.png)
### Putting It Together
- ![Putting It Together 1](images/putting_it_together_1.png)
- The following image gives us an intuitionf o what is happening as we are implementing our neural network:<br />
  ![Putting It Together 2](images/putting_it_together_2.png)
  - Ideally, you want h<sub>&Theta;</sub>(x<sup>(i)</sup>) &approx; y<sup>(i)</sup>. This will minimize our cost function. However, keep in mind that J(&Theta;) is not convex and thus we can end up in a local minimum instead.