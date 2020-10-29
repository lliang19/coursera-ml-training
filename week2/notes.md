# Week 2 Notes

## Multivariate Linear Regression

### Multiple Features
- Linear regression with multiple variables = "multivariate linear regression"
- x<sub>j</sub><sup>(i)</sup> = value of feature <i>j</i> in the <i>i<sup>th</sup></i> training example
- x<sup>(i)</sup> = the input (features) of the <i>i<sup>th</sup></i> training example
- m = the number of training examples
- n = the number of features
- Multivariable form of the hypothesis function
  - h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x<sub>1</sub> + &theta;<sub>2</sub>x<sub>2</sub> + &theta;<sub>3</sub>x<sub>3</sub> + ... + &theta;<sub>n</sub>x<sub>n</sub>
- We can think of this as &theta;<sub>0</sub> as the basic price of a house, &theta;<sub>1</sub> as the price per square meter, &theta;<sub>2</sub> as the price per floor, etc., with x<sub>1</sub> will be the number of square meters in the house, x<sub>2</sub> the number of floors, etc.
- We can then vectorize our hypothesis function for one training example:
  ![Hypothesis Function Vectorized](images/hypothesis_vectorization.png)
### Gradient Descent For Multiple Variables
- We repeat our gradient descent formula for 'n' features:
  ![Gradient Descent For Multiple Variables 1](images/gradient_descent_for_multiple_variables_1.png)
  ![Gradient Descent For Multiple Variables 2](images/gradient_descent_for_multiple_variables_2.png)
  ![Gradient Descent For Multiple Variables 3](images/gradient_descent_for_multiple_variables_3.png)
### Gradient Descent in Practice I – Feature Scaling
- We can speed up gradient descent by limiting/scaling our input values to roughly the same range
  - This works because &theta; will descend quickly on small ranges and slowly on large ranges, and it will oscillate inefficiently down to the optimum when the variables are very uneven.
  - Ideally, we want to modify the ranges of our input such that: -1 &le; x<sub>(i)</sub> &le; 1, or -0.5 &le; x<sub>(i)</sub> &le; 0.5
  - Not exact requirements, but it will help speed things up
- <b>Feature Scaling</b> and <b>Mean Normalization</b> are two techniques to help speed up gradient descent
  - Feature Scaling: involves dividing the input values by the range (max - min), which results in a new range of just 1
  - Mean Normalization: subtracting the average value for an input variable from the values for