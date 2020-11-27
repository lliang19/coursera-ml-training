# Week 4 Notes

## Neural Networks

### Model Representation I
- **Neurons** are basically computational units that take inputs (**dendrites**) as electrical inputs (called "spikes") that are channeled to outputs (**axons**)
  - In our model, dendrites are like the input features x<sub>1</sub>...x<sub>n</sub>, and the output is the result of our hypothesis function
  - In this model our x<sub>0</sub> input node is sometimes called the "bias unit", always equal to 1
- We use the same logistic function as in classification, 1 / (1 + e<sup>-&theta;<sup>T</sup>x</sup>), yet we sometimes call it a sigmoid (logistic) **activation** function
  - In this situation, our "theta" parameters are sometimes called "weights"
- Visually, a simplistic representation looks like:<br />
  ![Model Representation I 1](images/model_representation_i_1.png)
- Input nodes (layer 1), also known as the "input layer", go into another node (layer 2), and finally outputs the hypothesis function, known as the "output" layer"
  - We can have intermediate layers of nodes between the input and output layers called the "hidden layers"
  - We label these intermediate or "hidden" layer nodes a<sup>2</sup><sub>0</sub>...a<sup>2</sup><sub>n</sub> and call them "activation units"<br />
    ![Model Represetation I 2](images/model_representation_i_2.png)
- One hidden layer would look like:<br />
  ![Model Representation I 3](images/model_representation_i_3.png)
- Value for each activation node is as follows:<br />
  ![Model Representation I 4](images/model_representation_i_4.png)
  - This is saying that we compute our activation nodes by using a 3x4 matrix of parameters
    - Apply each row of the parameters to our inputs to obtain the value for one activation node
    - Our hypothesis output is the logistic function applied tot he sum of the values of our activations nodes, which have been multiplied by yet another parameter matrix &Theta;<sup>(2)</sup> containing the weights for our second layer of nodes
    - Each layer gets its own matrix of weights, &Theta;<sup>(J)</sup>
    - The dimensions of these matrices of weigths is determined as follows:<br />
    *If network has s<sub>j</sub> units in layer j and s<sub>j+1</sub> units in layer j+1, then &Theta;<sup>(j)</sup> will be of dimension s<sub>j+1</sub> x (s<sub>j</sub> + 1)*
- ![Model Representation I 5](images/model_representation_i_5.png)
### Model Representation II
- Taking our example of a neural network from the previous section, we can replace the parameters inside our g function with a new variable z<sub>k</sub><sup>(j)</sup> to get:<br />
  ![Model Representation II 1](images/model_representation_ii_1.png)
  - In other words, for layer j = 2 and node k, the variable z will be:<br />
    ![Model Representation II 2](images/model_representation_ii_2.png)
  - The vector representatin of x and z<sup>j</sup> is:<br />
    ![Model Representation II 3](images/model_representation_ii_3.png)
  - Setting x = a<sup>(1)</sup>, we can rewrite the equation as:<br />
    ![Model Representation II 4](images/model_representation_ii_4.png)
- We are multiplying our matrix &Theta;<sup>(j-1)</sup> with dimensions *s<sub>j</sub> x (n + 1)* (where s<sub>j</sub> is the number of our activation nodes) by our vector a<sup>(j-1)</sup> with height (n+1). This gives us our vector z<sup>(j)</sup> with height s<sub>j</sub>. Now we can get a vector of our activation nodes for layer j as follows:<br />
  *a<sup>(j)</sup> = g(z<sup>(j)</sup>)*
where our function g can be applied element-wise to our vector z<sup>(j)</sup>.
- We can then add a bias unit (equal to 1) to layer j after we have computed a<sup>(j)</sup>. This will be element a<sub>0</sub><sup>(j)</sup> and will be equal to 1. To compute our final hypotehsis, let's first compute another z vector:<br />
  z<sup>(j+1)</sup> = &Theta;<sup>(j)</sup>a<sup>(j)</sup>
- We get this final z vector by mulitplying hte next theta matrix after &Theta;(j-1) with the values of all the activation nodes we just got. This last theta matrix &Theta;<sup>(j)</sup> will have only **one row** which is multiplied by one column a<sup>(j)</sup> so that our result is a single number. We then get our final result with:<br />
  h<sub>&Theta;</sub>(x) = a<sup>(j+1)</sup> = g(z<sup>(j+1)</sup>)
  - Notice that in this **last step**, between layer j and layer j+1, we are doing **exactly the same thing** as we did in loigist regression. Adding all these intermediate layers in nerual networks allow us to more elegantly produce interesting and more complex linear hypothesis.

## Applications

### Examples and Intuitions I
- A simple example of a neural network is attempting to map out the logical AND function, where the output is 1 (or true) **only** when both x<sub>1</sub> and x<sub>2</sub> are both 1.
- The graph of our functions will look like:<br />
  ![Examples and Intuitions I 1](images/examples_and_intuitions_i_1.png)
  - Remember that x<sub>0</sub> is our bias variable and is always 1
- Let's set our first theta matrix as: &Theta;<sup>(1)</sup> = [-30 20 20]
- This will cause the output of our hypothesis to only be positive if both x<sub>1</sub> and x<sub>2</sub> are 1:<br />
  ![Examples and Intuitions I 2](images/examples_and_intuitions_i_2.png)
- The following is an example of the logical OR operator:<br />
  ![Examples and Intuitions I 3](images/examples_and_intuitions_i_3.png)
- Where g(z) is the following:<br />
  ![Examples and Intuitions I 4](images/examples_and_intuitions_i_4.png)
### Examples and Intuitions II
- ![Examples and Intuitions II 1](images/examples_and_intuitions_ii_1.png)
- And there we hav ethe XNOR operator using a hidden layer with two nodes! The following summarizes the above algorithm:<br />
  ![Examples and Intuitions II 2](images/examples_and_intuitions_ii_2.png)
### Multiclass Classification
- ![Multiclass Classification 1](images/multiclass_classification_1.png)