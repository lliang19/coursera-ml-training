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
  - ![Hypothesis Function Vectorized](images/hypothesis_vectorization.png)
- 