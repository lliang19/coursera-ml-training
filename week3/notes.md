# Week 3 Notes

## Classification and Representation

### Classification
- Classification problems are like regression problems, except the values we want to predict take on only a small number of discrete values
  - For now, focus on **binary classification problem**, where *y* can only take on two values, 0 and 1
### Hypothesis Representation
- To fix our hypothesis function to satisfy 0 &le; *h<sub>&theta;</sub>(x)* &le; 1, we plug *&theta;<sup>T</sup>x* into the Logistic Function
  - Our new form uses the "Sigmoid Function," also called the "Logistic Function:<br />
  ![Sigmoid Function 1](images/sigmoid_function_1.png)<br />
  ![Sigmoid Function 2](images/sigmoid_function_2.png)
  - The function g(z) maps any real number to the (0, 1) interval, since as z approaches negative infinity, g(z) = 0, and as z approaches positive infinity, g(z) = 1
- *h<sub>&theta;</sub>(x)* will then give us the **probability** that our output is 1, e.g.: *h<sub>&theta;</sub>(x)* = 0.7 tells us that we have a probability of 70% that our output is 1
  - The probability that our prediction is 0 is just the **complement** of our probability that it is 1<br />
  ![Hypothesis Probability](images/hypothesis_probability.png)
### Decision Boundary
- ![Decision Boundary 1](images/decision_boundary_1.png)
- **Decision Boundary**: the line that separates the area where y = 0 and where y = 1
  - Created by our hypothesis function
  - Example:<br />
   ![Decision Boundary 2](images/decision_boundary_2.png)
    - This decision boundary is a straight vertical line placed on the graph where *x<sub>1</sub>* = 5, with everything to the left denoting y = 1, and everything to the right denoting y = 0
  - The input to the sigmoid function g(z) (e.g. *&theta;<sup>T</sup>X*) doesn't need to be linear, could be a function that describes a circle (e.g. *z = &theta;<sub>0</sub> + &theta;<sub>1</sub>x<sub>1</sub><sup>2</sup> + &theta;<sub>2</sub>x<sub>2</sub><sup>2</sup>*) or any shape to fit our data

## Logistic Regression Model

### Cost Function
- For logistic regression, our cost function must be **convex**, or always having a global minimum and no local minimum. Therefore, our function will look like:<br />
  ![Cost Function 1](images/cost_function_1.png)
- ![Cost Function 2](images/cost_function_2.png)
- ![Cost Function 3](images/cost_function_3.png)
- Intuitively, if our correct answer *y* is 0 and we predict 0 (*h(x) = 0*), then our cost = 0. Similarly, if our correct answer *y* is 1 and we predict 1 (*h(x) = 1*), then our cost = 0.
- As our hypotheses approach 1 for y = 0 and/or 0 for y = 1, our const function will approach infinity
  - Note: writing our cost function in this way guarantees that J(&theta;) is convex for logistic regression
### Simplified Cost Function and Gradient Descent
- We can compress our cost function's two conditional cases into one case: *Cost(h<sub>&theta;</sub>(x),y) = -y log(h<sub>&theta;</sub>(x)) - (1 - y)log(1 - h<sub>&theta;</sub>(x))*
  - When y = 1, the second term will be 0 and will not affect the result, and similarly when y = 0, the first term will be 0 and will not affect the result
  - We can fully write out our cost function as follows:<br />
  ![Simplified Cost Function 1](images/simplified_cost_function_1.png)
  - A vectorized implementation is:<br />
  ![Simplified Cost Function 2](images/simplified_cost_function_2.png)
- ![Simplified Cost Function 3](images/simplified_cost_function_3.png)
### Advanced Optimization
- In order to use more sophisticated and highly optimized algorithms for computing &theta;, we can use Octave's native libraries to do so
- First, we need to provide a function that evaluates J(&theta;) (cost) and (d/d&theta;<sub>j</sub>)J(&theta;) (partial derivative of each term in &theta;)
  - We can write a single function that returns both of these:
  <pre><code>function [jVal, gradient] = costFunction(theta)
    jVal = [...code to compute J(theta)...];
    gradient = [...code to compute derivative of J(theta)...];
  end</code></pre>
  - We can then use Octave's "fminunc()" optimization algorithm along with the "optimset()" function that creates an object containing the options we want to send to "fminunc()":
  <pre><code>options = optimset('GradObj', 'on', 'MaxIter', 100);
  initialTheta = zeros(2,1);
     [optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options);</code></pre>
  - We give the function "fminunc()" our cost function, initial vector of theta values, and the "options" object that we created beforehand
 
## Multiclass Classification

### Multiclass Classification: One-vs-all
- Since y = {0, 1, ... n}, we divide our problem into n+1 (+1 because the index starts at 0) binary classification problems, each one we predict the probability that 'y' is a member of one of our classes (e.g. y = x for some class)
  - ![Multiclass Classification 1](images/multiclass_classification_1.png)
  - We are essentially choosing one class and lumping all the others into a single second class, and we do this repeatedly, applying binary logistic regression to each case, and then use the hypothesis that returned the highest value as our prediction
  - ![Multiclass Classification 2](images/multiclass_classification_2.png)

## Solving the Problem of Overfitting
- **Overfitting**: if we have too **many** features, the learned hypothesis may fit the training set very well, but fails to **generalize** well to predict on new data
- Addressing overfitting includes:
  - Reducing the number of features
    - Manually select which features to keep
    - Use a model selection algorithm (in later weeks)
  - Regularization
    - Keep all the features, but reduce the magnitude of parameters &theta;<sub>j</sub>
    - Regularization works well when we have a lot of slightly useful features
## Cost Function (Regularization)
- If we have overfitting from our hypothesis function, we can reduce the weight that some of the terms in our function carry by increasing their cost
- For example, say we wanted to make the hypothesis function more quadratic: *&theta;<sub>0</sub> + &theta;<sub>1</sub>x + &theta;<sub>2</sub>x<sup>2</sup> + &theta;<sub>3</sub>x<sup>3</sup> + &theta;<sub>4</sub>x<sup>4</sup>*
  - We will want to eliminate the influence of *&theta;<sub>3</sub>x<sup>3</sup>* and *&theta;<sub>4</sub>x<sup>4</sup>* without actually getting rid of those features or changing the form of our hypothesis:<br />
    ![Regularization Cost Function 1](images/regularization_cost_function_1.png)
  - ![Regularization Cost Function 2](images/regularization_cost_function_2.png)
- We could also regularize all of our theta parameters in a single summation:<br />
  ![Regularization Cost Function 3](images/regularization_cost_function_3.png)
- The &lambda; is the **regularization parameter** that determines how much the costs of our theta parameters are inflated
  - If lambda is too large, it may smooth out the function too much and cause underfitting, and if lambda is too small, it may not have much affect on regularizing our hypothesis function
 ### Regularized Linear Regression
 #### Gradient Descent
  - We modify our gradient descent function to separate out *&theta;<sub>0</sub>* from the rest of the parameters because we do not want to penalize *&theta;<sub>0</sub>*:<br />
    ![Regularized Linear Regression 1](images/regularlized_linear_regression_1.png)
  - The term *(&lambda;/m)&theta;<sub>j</sub>* performs our regularization, and with some manipulation our update rule can be represented as: <br />
    ![Regularized Linear Regression 2](images/regularized_linear_regression_2.png)
#### Normal Equation
- We can also approach regularization using the alternative method of the non-iterative normal equation. To add in regularization, the equation i the same as our original except that we add another term inside the parentheses:<br />
  ![Regularized Linear Regression 3](images/regularized_linear_regression_3.png)
  - This equation should have dimension (n+1) x (n+1), and when we add the term &lambda; * L, *X<sup>T</sup>X + &lambda; * L* becomes invertible (in the case that m < n where *X<sup>T</sup>X* is non-invertible)
### Regularized Logistic Regression
- Our cost function for logistic regression was:<br />
  ![Regularized Logistic Regression 1](images/regularized_logistic_regression_1.png)
  - We can regularize this equation by adding a term to the end:<br />
    ![Regularized Logistic Regression 2](images/regularized_logistic_regression_2.png)
  - The second sum &Sigma;<sup>n</sup><sub>j=1</sub> **means to explicitly exclude** the bias term *&theta;<sub>0</sub>*, since the &theta; vector is indexed from 0 to n
  - ![Regularized Logistic Regression 3](images/regularized_logistic_regression_3.png)