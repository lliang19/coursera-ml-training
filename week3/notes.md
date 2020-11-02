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
- 