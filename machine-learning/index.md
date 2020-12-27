# Machine Learning


![Machine-Learning](/Machine-Learning.jpg)

# Lecture by [Andrew Ng, Coursera](https://www.coursera.org/learn/machine-learning)

## Basic Concepts & Linear Regression 

### Supervised Learning vs. Unsupervised Learning

- Supervised Learning: 

  > In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.
  
  - Training Data already has the value, which our Function should predict for a new, strange input. i.e, In the case below, we want to get a function, so that we can calculate the price of a house to be sold. We have __4 Training Data__ in this table and each Data has 4 __Features__ that have a influence on its' price ( we call it as __Multi-Features__. It'll be discussed later:) ).

  - It's devided in __Regression__ and __Classification__ Problems
  

||Size|Number of Bedrooms|Number of Floors|Age(years)|Price(1000$)|
|:---:|:---------:|:----------------:|:--------------:|:--------:|:---:|
|$TrainingData_1$|2104|5|1|45|460|
|$TrainingData_2$|1416|3|2|40|232|
|$TrainingData_3$|1534|3|2|30|315|
|$TrainingData_4$|852|2|1|36|178|
|...|...|...|...|...|...|
||($x_1$)|($x_2$)|($x_3$)|($x_4$)|($x_5$)|

- Unsupervised Learning 
  
  > Unsupervised learning, on the other hand, allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

### Regression vs. Classification

- Regression: The Value we want to predict is __continious__ instead of discrete. E.g., the Price of a House.

    > In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function. 

- Classification: As its' name, we want to __devide the input in different classes__. E.g., After training, with the help of the <u>color, weight, outlook and smel</u> ( __Features__ ), we want to predict if the coffee beans we have come from Arabica or Robusta.

    > In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories.

### Linear Regression with 1 Variable / Feature

- Hypothesis Function

  - $\hat y = h_\theta = \theta_0 + \theta_1x$

- Cost Function

  - $J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^m(\hat y_i - y_i)^2$
    
    $\rarr J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^m(h_\theta(x_i) - y_i)^2$

- Optimize

  - __Gradient Descent.__ More specifically, repeat:
  
    $tmp_0 = \theta_0 - \alpha\frac{\partial}{\theta_0}{J(\theta_0, \theta_1)}$
    
    $\rarr tmp_0 = \theta_0 - \alpha\frac{1}{m}\sum_{i=1}^m{(h_\theta(x_i) - y_i)}$
    
    $tmp_1 = \theta_1 - \alpha\frac{\partial}{\theta_1}{J(\theta_0, \theta_1)}$
    
    $\rarr tmp_1 = \theta_1 - \alpha\frac{1}{m}\sum_{i=1}^m{((h_\theta(x_i) - y_i)x_1)}$
    
    $\theta_0 = tmp_0$
    
    $\theta_1 = tmp_1$

    We call $\alpha$ __Learning Rate.__ Its' value has influence on the speed, how fast we can find the parameters, with that we can reach a local optimal value.

  - __When $\alpha$ too large / too small is:__

    - too large: we might miss the parameters, which can help us get the local optimal value.

    - too small: We need more iterations ( Baby Steps / more time ).

    - We can make the judge, whether $\alpha$ too large / small ist by drawing the plot of __iterations - $J(\theta_0, \theta_1)$:__ It should be lower. Otherwise is $\alpha$ too large.
    - We can start $\alpha$ from __0.001, ..., 0.01, ..., 0.1.__ And Andrew Ng advises us to use 3 times ( 0.001, 0.003, 0.01, 0.03, 0.1 ) to try it.

### Multiple Features and Matrix

- Vector:

  - A vector is a Matrix with __one Column and many rows.__ E.g., $\begin{bmatrix}x_0 \\\\ x_1 \\\\x_2 \\\\x_3 \end{bmatrix}$

- Hypothesis:

  - We use the table above as example, we have 4 Training Data and each of them has 4 Features. According to this, we should have 4+1 parameters $\theta_0-\theta_4$. We write the Hypothesis below:
  
    $h_\theta(x^i) = \theta_0 + \sum_{j=1}^4\theta_jx_j^i$
  
    $x_i^j$ here means the _jth Feature_ of the _ith Training Data._

    Actually we can add a Feature $x_0 \equiv 1$, then we can use the Matrix. So that we can write the Equation above as below:
  
    $h_\theta(x^i) = \sum_{j=0}^4\theta_jx_j^i$

    We let:
    
    $\Theta = \begin{bmatrix}\theta_0, \theta_1, \theta_2, \theta_3, \theta_4\end{bmatrix}$, 
    
    $X = \begin{bmatrix}  x^1_0 & x^2_0 & x^3_0 & x^4_0 \\\\ x^1_1 & x^2_1 & x^3_1 & x^4_1 \\\\ x^1_2 & x^2_2 & x^3_2 & x^4_2 \\\\ x^1_3 & x^2_3 & x^3_3 & x^4_3 \\\\ x^1_4 & x^2_4 & x^3_4 & x^4_4 \end{bmatrix}$. 
    
    So that $h_\theta(x^i) = \Theta * i_{th}$ column of $X$. In Matrix $X$, element $x_0^i \equiv 1$. We can also calculate $\Theta * X$ directly, the $i_{th}$ colum is the value of $h_\theta(x^i)$.

- Cost Function:
  
  - Assume we have __m Training Data__, each of them has __n Features__.
  
    $J(\theta_0, \theta_1, ... \theta_n) = \frac{1}{2m}\sum_{i=1}^m(h_\theta(x^i) - y^i)^2$

- Gradien Descent:

  - repeat:
  
    $tmp_i = \theta_i - \alpha\frac{\partial}{\partial\theta_i}J(\theta_0, \theta_1, ..., \theta_n)$ 
    
    $\rarr tmp_i = \theta_i - \alpha\frac{1}{m}\sum_{i=1}^m(h_\theta(x^i) - y^i)* x^i)$

    $\theta_i = tmp_i$

### Feature Scaling

- We use this technique __when the range of Features have great Difference.__ E.g., $0 \leq x_1 \leq 2000, 0 \leq x_2 \leq 5$, then we can $x_1 \coloneqq \frac{x_1}{2000}, x_2 \coloneqq \frac{x_2}{5}.$ This helps with the speed up of the Gradient Descent.

- Andrew Ng advices that scaling all Features __approximately__ into the range __[-1, 1]__.

- We can also scale the Features by using this:
  
  $x_i = \frac{x_i - \mu_i}{s_i}$

  Here $\mu_i$ is the average value of Feature $x_i$, $s_i$ is normally $value_{max} - value_{min}$. 

### Normal Equation

- The Method to solve for $\Theta$ analytically:
  
  $\Theta = (X^TX)^{-1}X^Ty$ can minimize the $J(\theta)$.

  $x^i = \begin{bmatrix}x_0^i, x_1^i, ..., x_n^i\end{bmatrix}$

  $X = \begin{bmatrix} x_0^1 & x_1^1 & {...} & x_n^1 \\\\ x_0^2 & x_1^2 & {...} & x_n^2 \\\\ ... & ... & ... & ... \\\\x_0^m & x_1^m & {...} & x_n^m \end{bmatrix}$

  In this Matrix, we write __each row the Features of one Training Data__.
  
  $y = \begin{bmatrix}y^{(1)}\\\\...\\\\y^{(m)}\end{bmatrix}$

- Suppose $m \leq n$, then is $X^TX$ is degenerated.

- The following table can helps us decide, when to use __Normal Equation__, when to use __Gradient Descent__.

  |Normal Equation|Gradient Descent|
  |:-------------:|:--------------:|
  |No need to choose $\alpha$.|May have "Baby Step" issue, or miss the local optimal value when $\alpha$ too large.|
  |Can be slow when __n ( Number of Features )__ too large is.|Works fine even when n large is.|
  |Some Matrix is __singular or degenerated.__||
  |$n \leq 10,000$|$n > 10,000$|

- Reasons of uninvertibility of Matrix $(X^TX)^{-1}$:
  
  - Redundant Elements: linear depent.
  
    E.g., $x_1 = $size in $feet^2$, $x_2$ = size in $m^2$.
  
- Too many Features: Just delete some of them, or use __regulization ( discuss later ).__

## Logistic Regression & Overfitting & Regularization 

### Logistic Regression - Classification

  - Examples: Email (Spam / Not Spam), Online Transactions: Fraudulent ( Yes / No ) ?
  
  - $y \isin {0, 1} \begin{cases} 0 &\text{Negative Class} \\\\ 1 &\text{Positive Class} \end{cases}$

  - p.s. In __multi-class__ Prolems this set can have more than 2 elements.

- What if we use linear Regression in a classfication problem?
  
  - $h_\theta(x) = \theta^Tx< 0$ or $> 1$

- In __Logistic Regression__, it shouled always be: __$0 \leq h_\theta(x) \leq 1$__. So we do the following transformation, then we get the __Hypothesis__:

  - $h_\theta(x) = g(\theta^Tx)$

  - Then we use __Sigmoid Function / Logistic Function:__ 

    - $g(z) = \frac{1}{1 + e^{-z}}$
    
    ![Sigmoid](/Sigmoid.png)

  - We have now:
    
    - $h_\theta(x) = \frac{1}{1 + e ^ {-\theta^Tx}}$

  - This Function $h_\theta(x)$ comes out the result that estimated probability that $y = 1$ on input x. We can also write it in the following Form:
    
    $h_\theta(x) = P(y = 1 | x; \theta)$ $\rarr$ Probability that $y = 1$, given $x$, parameterized by $\theta$.

  - $P(y = 1 | x; \theta) + P(y = 0 | x; \theta) = 1$

### Deciding Boundary 
  
- Linear

  ![Linear](/Linear.png)

- Non-Linear

  ![Non-Linear](/Non-Linear.png)

### Cost Function

- Training Set: ${(x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), ..., (x^{(m)}, y^{(m)})}$, __m examples__

- x $\isin \begin{bmatrix}x_0 \\\\ x_1 \\\\ ... \\\\ x_m\end{bmatrix}, x_0 \equiv 1, y \isin (0, 1)$

- $h_\theta(x) = \frac{1}{1 + e ^ {-\theta^Tx}}$

  > Brief Review: Cost Function in __Linear Regression:__  
    $J(\theta) = \frac{1}{m}\sum_{i=1}^m\frac{1}{2}(h_\theta(x^{(i)} - y^{(i)})^2$  
    $Cost(h_\theta(x), y) = \frac{1}{2}(h_\theta(x) - y)^2$

- $Cost(h_\theta(x), y) = \begin{cases}-log(h_\theta(x))&\text{if y = 1}\\\\-log(1 - h_\theta(x)) &\text{if y=0}\end{cases}$

  - if $y = 1, h_\theta(x) = 1 \rarr Cost = 0$.

  - But as $h_\theta(x) \rarr 0, Cost \rarr \infty$

    Predict $P(y=1|x; \theta) = 0$, but $y = 1$, we'll penalize learning algorithm by a very large cost.

- We can also write it like below:

  - $Cost(h_\theta(x), y) = -ylog(h_\theta(x)) - (1-y)log(1 - h_\theta(x))$

![Logistic-Cost-Function](/Logistic-Regression-cost-function.png)

### Gradient Descent

- $J(\theta) = \frac{1}{m}\sum_{i=1}^mCost(h_\theta(x^{(i)}), y^{(i)})$
  
  $\rarr J(\theta) = -\frac{1}{m}[\sum_{i=1}^my^{(i)}log(h_\theta(x^{(i)}) - y^{(i)}) + (1 - y^{(i)})log(1 - h_\theta(x^{(i)}))]$

- Repeat:
  
  $\theta_j := \theta_j - \alpha\frac{\partial}{\partial\theta_j}J(\theta)$

  $\rarr \theta_j := \theta_j - \alpha\frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})x^{(i)}_j$

  __It looks identical to Linear Regression. BUT:__

    - $h_\theta(x) = \theta^Tx$ in Linear Regression
    
    - In Logistic Regression is $h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx}}$

- __Try to write it out:__

### Anvanced Optimization

- Algorithms:
  
  - ~~Gradient Descent~~
  
  - Conjugate gradient
  
  - BFGS
  
  - L-BFGS

  Advantages:

  - No need to manually choose $\alpha$
  
  - Often faster than gradient descent

  Disadvantages:

  - More complex

### Multi-class Classification: one-vs-all ( one-vs-rest )

- E.g., Email foldering / tagging: Work, Friends, Family, Hobby ($y=1, y=2, y=3, y=4$)

- $h_\theta^{(i)} = P(y = i | x; \theta)$ $(i=1,2,3)$

- Train a logistic regression classifier $h_\theta^{(i)}(x)$ for each class $i$ to predict the probability that $y=i$. On a new input $x$, to make a prediction, pick the class $i$ that maximizes $max_ih_\theta^{(i)}(x)$.

![multiclass.png](/multiclass.png)

### Overfitting

#### Definiation

- If we have too many Features, the learned hypothesis may __fit the training set very well, but fail to generalize to new examples__. $\darr$

![Overfitting.png](/Overfitting.png)

- On Logistic Regression $\darr$

![Overfitting-Logistic.png](/Overfitting-Logistic.png)

#### Adressing Overfitting:
  
  1. __Reduce number of Features__
     
     - Manually select which Features to keep
     
     - Model selection algorithm
  
  2. __Regularization__
     
     - Keep all the Features, but reduce magnitude / values of parameters $\theta$.
     
     - Works well when we have a lot of Features, each of which contributes a bit to predicting $y$.

### Regularization

- Small Values for parameters $\theta_0, \theta_1, ..., \theta_n$
  
  - "Simpler" hypothesis
  
  - Less prone to overfitting

- E.g. Housing:
  
  - Features: $x_1, x_2, ..., x_{100}$
  
  - Parameters: $\theta_0, \theta_1, ..., \theta_n$
  
  - $J(\theta) = \frac{1}{2m}[\sum_{i=1}^m(h_\theta(x^{(i)} - y^{(i)})^2 + \lambda\sum_{j=1}^{n}\theta_j^2]$. We pinelize only $\theta_{i > 0}$
     
  - $\lambda\sum_{j=1}^{n}\theta_j^2$ is called Regulization Parameter.
  
  - When the $\lambda$ too large is, $h_\theta(x) = \theta_0$ (Because this can make $\theta_{i > 0} \thickapprox 0$)

#### Regularized Linear Regression

  - __Cost Function:__
    
    - $J(\theta) = \frac{1}{2m}[\sum_{i=1}^m(h_\theta(x^{(i)} - y^{(i)})^2 + \lambda\sum_{j=1}^{n}\theta_j^2]$.
  
  - __Gradient Descent:__
  
    - $\theta_0 := \theta_0 - \alpha \frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})(x_0 \equiv 1))$
  
    - $\theta_{j > 0} := \theta_j - \alpha[\frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)} - y^{(i)}))x^{(i)} + \frac{\lambda}{m}\theta_j]$
    
      $\rarr \theta_{j > 0} := \theta_j(1- \alpha\frac{\lambda}{m}) - \alpha\frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)} - y^{(i)}))x^{(i)}$

    - In the Equation above, $ \theta_j(1- \alpha\frac{\lambda}{m}) < 1$. We can be sure that the parameter will be smaller in each iteration.

- __Normal Equition:__

  - $X = \begin{bmatrix}(x^{(i)})^T\\\\...\\\\(x^{(m)})^T\\\\\end{bmatrix}$
  
  - $y = \begin{bmatrix}y^{(1)}\\\\...\\\\y^{(m)}\end{bmatrix}$

  - $\theta = (X^TX + \lambda\begin{bmatrix}0 & 0 & 0\\\\0 & 1 &0 \\\\ 0 & 0 & 1\end{bmatrix})^{-1}X^Ty$
    
    - The Elements in the Matrix next to $\lambda$ looks like: $e_{i = j\not = 0}$

#### Regularized Logistic Regression

- __Cost Function:__
  
  - $J(\theta) = -[\frac{1}{m}\sum_{i=1}^my^{(i)}logh_\theta(x^{(i)}) + (1 - y^{(i)})log(1 - h_\theta(x^{(i)}))] + \frac{\lambda}{2m}\sum_{j=1}^m\theta_j^2$

- __Gradient Descent:__
  
  - $\theta_0 := \theta_0 - \alpha \frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})(x_0 \equiv 1))$  
  
  - $\theta_{j > 0} := \theta_j - \alpha[\frac{1}{m}\sum_{i=1}^m(h_\theta(x^{(i)} - y^{(i)}))x^{(i)} + \frac{\lambda}{m}\theta_j]$
  
  - Here $h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx}}$

## Non-Linear Hypothesis - Neural Networks

- What should we do when we proceed an Image?

  - Transfer it into a grayscale-image. It has only $\frac{1}{3}$ Features that RGB-image has.

### Neural Network

- Origins: Algorithms that try to mimic the brain.

- Neuron Model: Logistic Unit

  $x = \begin{bmatrix}x_0\\\\x_1\\\\...\\\\x_n\end{bmatrix}$ (Just a Vector of Features.)

  $\theta = \begin{bmatrix}\theta_0\\\\\theta_1\\\\...\\\\\theta_n\end{bmatrix}$

  ![Logistic Unit.jpg](/Logistic%20Unit.jpg)

  In this Picture, $x_0$ is called __the bias unit__ or __the bias neuron.__ And $x_0 \equiv 1$

  There's a __sigmoid(logistic) Activaition Function__ in this Picture 

#### Presentations:

![NN.png](/NN.png)

- $a_i^{(j)}: $ Activation of Unit $i$ in Layer $j$

- $\Theta^{(j)}: $ Matrix of weights controlling function mapping from layer $j$ to layer $j+1$

- :warning: If networks has $s_j$ units in layer $j$, $s_{j+1}$ Units in layer $j+1$, then $\Theta^{(j)}$ will be of dimension $s_{j+1} \times (s_j + 1)$. 
  __And it should be randomly intialized.__

#### Vectorized Implementation & Forward Propagation:

- $x = \begin{bmatrix}x_0\\\\x_1\\\\x_2\\\\x_3\end{bmatrix}$

  $z^{(2)} = \begin{bmatrix}z_1^{(2)}\\\\z_2^{(2)}\\\\z_3^{(2)}\end{bmatrix}$

  $z^{(2)} = \Theta^{(1)}x$

  - We can image Input Layer as $a^{(1)}$. Then we can write in this Form:
  
    $z^{(2)} = \Theta^{(1)}a^{(1)}$
  
  $a^{(2)} = g(z^{(2)})$ (Here $g$ is the Sigmoid Function.)

  - Add $a_0^{(2)} = 0$

  $z^{(3)} = \Theta^{(2)}a^{(2)}$

  $h_\theta(x) = a^{(3)} = g(z^{(3)})$

- We can through choosing $\theta$ to realize _AND, OR, NOT, XOR, XNOR_...

### Cost Function

#### Definitions:
  
  - Training Datas: ${(x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), ..., (x^{(m)}, y^{(m)})}$
  
  - $L = $ total no. of Layers in network
  
  - $s_l = $ no. of units ( not counting bias unit ) in layer $l$.
  
#### Classification Problems:

|Binary Classification|Multi-class Classification ( K classes ) |
|:-------------------:|:---------------------------------------:|
|$y = 0$ or $1$|$y \isin \R^K$, E.g. $\begin{bmatrix}1\\\\0\\\\0\\\\0\end{bmatrix}$, $\begin{bmatrix}0\\\\1\\\\0\\\\0\end{bmatrix}$, $\begin{bmatrix}0\\\\0\\\\1\\\\0\end{bmatrix}$, $\begin{bmatrix}0\\\\0\\\\0\\\\1\end{bmatrix}$|
|1 output unit|K output units|

#### Logistic Regression:

  > Brief Review:  
  $J(\theta) = -\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}log(h_\theta(x^{(i)})) + (1 - y^{(i)})log(1 - h_\theta(x^{(i)}))] + \frac{\lambda}{2m}\sum_{j=1}^{n}\theta_j^2$

  - Neural Network:

    $h_\Theta(x) \isin \R^K, (h_\Theta(x))_i = i^{th}$ Output

    $J(\Theta) = -\frac{1}{m}[\sum_{i=1}^{m}\sum_{k=1}^{K}y_k^{(i)}log(h_\Theta(x^{(i)}))_k + (1 - y_k^{(i)})log(1 - (h_\Theta(x^{(i)}))_k)] + \frac{\lambda}{2m}\sum_{l = 1}^{L - 1}\sum_{i = 1}^{s_l}\sum_{j = 1}^{s_{l+1}}(\Theta_{ji}^{l})^2$

### Backpropagation Algorithm

- Gradiet Descent, we need to compute:
  
  - $J(\Theta)$
  
  - $\frac{\partial}{\partial\Theta_{ij}^{(l)}}J(\Theta)$

  > $J(\Theta) = -\frac{1}{m}[\sum_{i=1}^{m}\sum_{k=1}^{K}y_k^{(i)}log(h_\Theta(x^{(i)}))_k + (1 - y_k^{(i)})log(1 - (h_\Theta(x^{(i)}))_k)] + \frac{\lambda}{2m}\sum_{l = 1}^{L - 1}\sum_{i = 1}^{s_l}\sum_{j = 1}^{s_{l+1}}(\Theta_{ji}^{l})^2$

- Intuition:

  - $\delta_j^{(l)}$ = "error" of node $j$ in layer $l$.
  
  - For each output Unit ( Layer = 4 ):
  
    $\delta_j^{(4)} = a_j^{(4)} - y_j$

    $a_j^{(4)} = (h_\theta(x))_j$

    We have: $\delta^{(4)} = a^{(4)} - y$

  - Then we execute the following Operations:

    $\delta^{(3)} = (\Theta^{(3)})^T\delta^{(4)} .* g'(z^{(3)})$

    $\delta^{(2)} = (\Theta^{(2)})^T\delta^{(3)} .* g'(z^{(2)})$

    Here $g'(z^{(n)}) = a^{(n)} .* (1 - a^{(n)})$

- Specifically:

  - Training Set: ${(x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), ..., (x^{(m)}, y^{(m)})}$
  
  - Set $\Delta_{ij}^{(l)} = 0$, for all $i, j, l$
  
  - For $i = 1$ to $m$:
  
      Set $a^{(1)} = x^{(i)}$
  
      Perform forward propagation to compute $a^{(l)}$ for $l = 2, 3, ..., L$
  
      Using $y^{(i)}$, compute $\delta^{(L)} = a^{(L)} - y^{(i)}$
  
      Compute $\delta^{(L - 1)}, \delta^{(L - 2)}, ..., \delta^{(2)}$
  
      $\Delta_{ij}^{(l)}:= \Delta_{ij}^{(l)} + a_j^{(l)}\delta_i^{(l+1)}$
  
  - $D_{ij}^{(l)} := \frac{1}{m}\Delta_{ij}^{(l)} + \lambda\Theta_{ij}^{(l)}$ if $j \neq 0$
  
  - $D_{ij}^{(l)} := \frac{1}{m}\Delta_{ij}^{(l)}$ if $j = 0$

### Evaluating Hypothesis

- Split the labeled data __randomly__ into 2 Parts: Training Set ( 70% ) and Test Set ( 30% ).

- Learn the parameter $\theta$ from Training data

- Computing test Set error:
  
  - In Linear Regression: $J(\theta) = \frac{1}{2m_{test}}\sum_{i = 1}^{m_{test}}(J(x_{test}^{(i)}) - y_{test}^{(i)})^2$
  
  - In Logistic Regression: $J(\theta) = =-\frac{1}{m_{test}}\sum_{i = 1}^{m_{test}}[y^{(i)}logh_{\theta}(x^{(i)}_{test}) + (1 - y^{(i)})log(1 - h_{\theta}(x^{(i)}_{test}))]$

- Misclassification error ( 0/1 multiclassification error ):

  - $err(h_{\theta}(x), y) = 1$, if $h_{\theta}(x) \leq 0.5, y = 1 | h_{\theta}(x) \geq 0.5, y = 0$
  - $Test_{error} = \frac{1}{m_{test}}\sum_{i = 1}^{m_{test}}err(h_{\theta}(x_{test}^{(i)}), y^{(i)})$

### Model Selection, Training, Validation and Test

#### Model Selection

  1). $h_{\theta}(x) = \theta_0 + \theta_1(x) \rarr \theta^{(1)} \rarr J_{test}(\theta^{(1)})$
  
  2). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) \rarr \theta^{(2)} \rarr J_{test}(\theta^{(2)})$
  
  3). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) + \theta_3^3(x) \rarr \theta^{(3)} \rarr J_{test}(\theta^{(3)})$
  
  ...
  
  10). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) + \theta_3^3(x) + ... + \theta_{10}^{10}(x) \rarr \theta^{(10)} \rarr J_{test}(\theta^{(10)})$

- We should't use the chosen $\theta^{(5)}$ to test how well it fits in our Test Set. Because we become it from Training Set, and the Test Set has the same Dimension as the Training Set. __It lacks of Generalization on New Data Set.__

- Thus, we split the Data Set into 3 pieces: __Training Set ( 60% ), Cross Validation Set ( 20% ), Test Set ( 20% )__.

#### Train ( Books ) / Validation ( Homework ) / Test Error ( Examination )

- Training Error
  
  - $J_{train}(\theta) = \frac{1}{2m_{train}}\sum_{i = 1}^{m_{train}}(h_{\theta}(x_{train}^{(i)}) - y_{train}^{(i)})^2$

- Validation Error

  - $J_{cv}(\theta) = \frac{1}{2m_{cv}}\sum_{i = 1}^{m_{cv}}(h_{\theta}(x_{cv}^{(i)}) - y_{cv}^{(i)})^2$

- Test Error

  - $J_{test}(\theta) = \frac{1}{2m_{test}}\sum_{i = 1}^{m_{test}}(h_{\theta}(x_{test}^{(i)}) - y_{test}^{(i)})^2$

  1). $h_{\theta}(x) = \theta_0 + \theta_1(x) \rarr \theta^{(1)} \rarr J_{cv}(\theta^{(1)})$
  
  2). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) \rarr \theta^{(2)} \rarr J_{cv}(\theta^{(2)})$
  
  3). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) + \theta_3^3(x) \rarr \theta^{(3)} \rarr J_{cv}(\theta^{(3)})$
  
  ...
  
  10). $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) + \theta_3^3(x) + ... + \theta_{10}^{10}(x) \rarr \theta^{(10)} \rarr J_{cv}(\theta^{(10)})$

  Pick $h_{\theta}(x) = \theta_0 + \theta_1(x) + \theta_2^2(x) + \theta_3^3(x) + \theta_4^4(x)$, Estimate generalization error for test set $J_{test}(\theta^{(4)})$

#### Diagnosing Bias ( Too high -> underfit ) vs. variance ( Too high -> overfit )

- Training Error

  - $J_{train}(\theta) = \frac{1}{2m_{train}}\sum_{i = 1}^{m_{train}}(h_{\theta}(x_{train}^{(i)}) - y_{train}^{(i)})^2$

- Validation Error

  - $J_{cv}(\theta) = \frac{1}{2m_{test}}\sum_{i = 1}^{m_{cv}}(h_{\theta}(x_{cv}^{(i)}) - y_{cv}^{(i)})^2$

- Draw the __"Degree of polynomioal d - Error" plot.__ In this Plot draw the $J_{train}(\theta), J_{cv/test}(\theta)$. Then we can make sure wether it's high bias or high variance.

![Bias and Variance](/Bias%20and%20Variance.jpeg)

- Bias ( Underfit, when d too small ):
  
  - $J_{train}(\theta)$ will be high
  
  - $J_{train}(\theta) \approx J_{cv}(\theta)$

- Variance ( Overfit, when d too large ):

  - $J_{train}(\theta)$ will be low
  
  - $J_{cv}(\theta) \gg J_{train}(\theta)$

#### Regularization and bias / variance

- Linear Regression with Regularization

  Model: $h_{\theta}(x) = \theta_0 + \theta_1x + \theta_2x^2 + \theta_3x^3 + \theta_4x^4$

  Goal: $J(\theta) = \frac{1}{2m}\sum_{i = 1}^m(h_\theta(x^{(i)}) - y^{(i)})^2 + \frac{\lambda}{2m}\sum_{j = 1}^n\theta_j^2$
  
  $J_{train}(\theta) = \frac{1}{2m_{train}}\sum_{i = 1}^{m_{train}}(h_{\theta}(x_{train}^{(i)}) - y_{train}^{(i)})^2$

  $J_{cv}(\theta) = \frac{1}{2m_{cv}}\sum_{i = 1}^{m_{cv}}(h_{\theta}(x_{cv}^{(i)}) - y_{cv}^{(i)})^2$

  $J_{test}(\theta) = \frac{1}{2m_{test}}\sum_{i = 1}^{m_{test}}(h_{\theta}(x_{test}^{(i)}) - y_{test}^{(i)})^2$

- Chossing the parameter $\lambda$

  1). Try $\lambda = 0 \rarr minJ(\theta) \rarr \theta^{(1)} \rarr J_{cv}(\theta^{(1)})$

  2). Try $\lambda = 0.01 \rarr minJ(\theta) \rarr \theta^{(2)} \rarr J_{cv}(\theta^{(2)})$

  3). Try $\lambda = 0.02 \rarr minJ(\theta) \rarr \theta^{(3)} \rarr J_{cv}(\theta^{(3)})$

  4). Try $\lambda = 0.04 \rarr minJ(\theta) \rarr \theta^{(4)} \rarr J_{cv}(\theta^{(4)})$

  5). Try $\lambda = 0.08 \rarr minJ(\theta) \rarr \theta^{(5)} \rarr J_{cv}(\theta^{(5)})$

  ...

  10). Try $\lambda = 10 \rarr minJ(\theta) \rarr \theta^{(10)} \rarr J_{cv}(\theta^{(10)})$

  Pick $\theta^{(5)}$, Test Error: $J_{test}(\theta^{(5)})$

- Draw the __"lambda - Error" plot.__ In this Plot draw the $J_{train}(\theta), J_{cv/test}(\theta)$.

- When $\lambda$ too large:
  
  - $J_{train}(\theta)$ will be high
  
  - $J_{train}(\theta) \approx J_{cv}(\theta)$

- When $\lambda$ too small:

  - $J_{train}(\theta)$ will be low
  
  - $J_{cv}(\theta) \gg J_{train}(\theta)$

- __The Situation is contrary to the Dimension d.__

![Bias_lambda](/Bias_lambda.png)

#### Learning Curves

- $J_{train}(\theta) = \frac{1}{2m_{train}}\sum_{i = 1}^{m_{train}}(h_{\theta}(x_{train}^{(i)}) - y_{train}^{(i)})^2$

  $J_{cv}(\theta) = \frac{1}{2m_{cv}}\sum_{i = 1}^{m_{cv}}(h_{\theta}(x_{cv}^{(i)}) - y_{cv}^{(i)})^2$

- Draw the __"m ( size of Training Set ) - Error" plot.__ Reduce $m$ artificially.

- __Training Set Error will increase when m increases, and the Cross Validation Error will decrease on the contrary.__

- High Bias:

![high_bias](/high_bias.png)

- High Variance:

![high_variance](/high_variance.png)

  __Watch the Gap!__ ( Between $J_{train}(\theta), J_{test}(\theta)$)

#### How to deal with high Bias & high Variance?

|high Bias|high Variance|
|:-------:|:-----------:|
|Getting additional Features|Getting more Training examples|
|Try adding polynomial Features|Try smaller sets of Features|
|Try decreasing $\lambda$|Try increasing $\lambda$|

## Error Analysis

### Recommand Approach

- Start with a simple algorithm that you can implement quickly. Implement it and test it on Cross-Validation Set.

- Plot learning curves to decide if more Data, more Features, etc.

- Error Analysis: Manually examine the examples ( In __Cross Validation Set__ ) that your algorithm made errors on. See if you  spot any systematic trend in what type of examples it is making errors on.

### Error metrics for skewed classes

- Cancer classification example:

  - Train logistic regression model $h_\theta(x). ( $y = 1$ if cancer )
  
  - Find you got $1\%$ error on test set
  
  - Only $0.50\%$ patients have cancer
    
    ```
    function y = predictCancer(x)
      y = 0; // ignore x! Because 99.5% Patients don't have cancer!
    return
    ```
#### Precision / Recall

||1|0|
|:-:|:-:|:---:|
|1|True positiv|False positiv|
|0|False Negative|True Negative|

- Precision( Of all patients where we predicted $y = 1$, what fraction actually has cancer? )
  
  $\frac{True positives}{\#predicted Positive} = \frac{True positives}{True Pos + False Pos}$

- Recall( Of all patients that actually have cancer, what fraction did we corrently detect as having cancer? )
  
  $\frac{True positives}{\#actual Positives} = \frac{True Positives}{True Pos + False Neg}$

#### Trading off precision and recall

- Logistic Regression: $0 \leq h_\theta(x) \leq 1$
  Predict 1 if $h_\theta(x) \geq 0.5$
  Predict 0 if $h_\theta(x) \leq 0.5$
- Suppose we want to predict $y = 1$ ( cancer ) only if very confident

  $\rarr \text{Higher Precision, lower Recall}$

- Suppose we want to avoid missing too many cases of cancer ( avoid false Negatives )

  $\rarr \text{Higher Recall, lower Precision}$

- More generally, predict 1 if $h_\theta(x) \geq \text{threshold}$

  ![precision-recall](/precision-recall.png)

#### F Score

- How to compare Precision / Recall numbers?

||Precision (P)|Recall (R)|F Score|
|:-:|:--------:|:--------:|:-----:|
|Algorithm 1|0.5|0.4|0.444|
|Algorithm 2|0.7|0.1|0.175|
|Algorithm 3|0.02|1|0.0392|

- __F Score:__ $2\frac{PR}{P + R}$

## Support Vector Machines

### Optimization objective

> Brief Review of Logistic Regression  
  $h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx}}$  
  if $y = 1$, we want $h_\theta(x) \approx 1, \theta^Tx \gg 0$  
  if $y = 0$, we want $h_\theta(x) \approx 0, \theta^Tx \ll 0$  
  $J(\theta) = -\frac{1}{m}\sum_{i = 1}^{m}[y^{(i)}log(h_\theta(x^{(i)})) + (1 - y^{(i)})log(1 - h_\theta(x^{(i)}))] + \frac{\lambda}{2m}\sum_{j = 1}^{n}\theta_j^2$  
  
- $-log\frac{1}{1 + e^{-x}} \rarr Cost_1(\theta^Tx^{(i)})$
  
  ![logsigmoid](/logsigmoid.png)

- $-log(1 - \frac{1}{1 + e^{-x}}) \rarr Cost_0(\theta^Tx^{(i)})$

  ![-logsigmoid](/-logsigmoid.png)

#### Cost Function:

- We use a new function to replace $-log\frac{1}{1 + e^{-x}} \text{and} -log(1 - \frac{1}{1 + e^{-x}})$. We name they as $Cost_1(\theta^Tx^{(i)})\text{and}Cost_0(\theta^Tx^{(i)})$. Then the Cost Function in SVM is:

  $\frac{1}{m}\sum_{i = 1}^{m}[y^{(i)}Cost_1(\theta^Tx^{(i)}) + (1 - y^{(i)})Cost_0(\theta^Tx)] + \frac{\lambda}{2m}\sum_{j = 1}^{n}\theta_j^2$  

  __The following Plot is the Picture of 2 new Functions:__

  ![SVM](/SVMcost.jpeg)

  __Our goal is to minimize the following Function:__

  $min_\theta C\sum_{i = 1}^{m}[y^{(i)}Cost_1(\theta^Tx^{(i)}) + (1 - y^{(i)})Cost_0(\theta^Tx)] + \frac{1}{2}\sum_{j = 1}^{n}\theta_j^2$  

#### SVM Hypothesis:

- $h_\theta(x) = \begin{cases}1, \theta^Tx \geq 0\\\\0, \theta^Tx < 0\end{cases}$

### Large Margin Intuition

- Take a look at the Plot of the new Cost Functions:
  - if $y = 1$, we want $\theta^Tx \geq 1$
  - if $y = 0$, we want $\theta^Tx \leq -1$

#### SVM Decision Boundary

- $min_\theta C\sum_{i = 1}^{m}[y^{(i)}Cost_1(\theta^Tx^{(i)}) + (1 - y^{(i)})Cost_0(\theta^Tx^{(i)})] + \frac{1}{2}\sum_{j = 1}^{n}\theta_j^2 ( C = \frac{1}{\lambda} )$

  - __Large C: lower Bias, higher Variance__
  - __Small C: higher Bias, lower Variance__

- In "Large Margin Boundary" we know, we just have to optimize the following function:

  $\frac{1}{2}\sum_{j = 1}^{n}\theta_j^2$ ( Because the front part can be 0. )

  ![margin](/margin.png)

### Kernels

#### Kernel Function

- Given x,:
  
  $f_i = similarity(x, l^{(i)}) = exp(-\frac{||x - l^{(2)}||^2}{2\sigma^2})$

- Large $\sigma^2$: Features $f_i$ vary very smmothly: __Higher Bias, lower Variance__
- Small $\sigma^2$: Features $f_i$ vary very smmothly: __lower Bias, higher Variance__

#### SVM with Kernels

- Where to get $l^{(1)}, l^{(2)}, l^{(3)} ... ?$

  - Given $(x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), ..., (x^{(m)}, y^{(m)})$
  
  - Choose $l^{(1)} = x^{(1)}, l^{(2)} = x^{(2)}, ..., l^{(m)} = x^{(m)}$

- Given $x$:

  $f_1 = similarity(x, l^{(1)})$

  $f_2 = similarity(x, l^{(2)})$

    ...

  $f = \begin{bmatrix}f_0\\\\f_1\\\\f_2\\\\...\\\\f_m\end{bmatrix}, f_0 = 1$

- For Training example $(x^{(i)}, y^{(i)}):$

  $f_1^{(i)} = similarity(x^{(i)}, l^{(1)})$

  $f_2^{(i)} = similarity(x^{(i)}, l^{(2)})$

  $f_3^{(i)} = similarity(x^{(i)}, l^{(3)})$

  ...

  $f_m^{(i)} = similarity(x^{(i)}, l^{(m)})$

  $f^{(x)} = \begin{bmatrix}f_0^{(i)}\\\\f_1^{(i)}\\\\...\\\\f_m^{(i)}\end{bmatrix}$

- Predict $y = 1, \text{if } \theta^Tf \geq 0$ 

- Training: $min_\theta C\sum_{i = 1}^{m}[y^{(i)}Cost_1(\theta^Tf^{(i)}) + (1 - y^{(i)})Cost_0(\theta^Tf^{(i)})] + \frac{1}{2}\sum_{j = 1}^{n}\theta_j^2$

### Logistic Regression vs. SVMs

- n = number of Features, m = number of Training examples

- if n is large ( relative to m ):

  Use logistic Regression, or SVM without a kernel

- if n is small, m is intermediate:

  Use SVM with Gaussian Kernel

- if n is small, m is large:

  Create / Add more Features, then use logistic regression or SVM without a Kernel

## Unsupervised Learning

### Clustering

#### K-Mean Algorithm

- Input:
  
  - K ( Number of clusters )
  
  - Training Set $\{x^{(1)}, x^{(2)}, ..., x^{(m)}\}$
  
  - $x^{(i)} \isin \R^n$ ( Drop $x_0 = 1$ convention )

- Randomly initialize K cluster Centroids $\mu_1, \mu_2, ..., \mu_k\isin\R^n$

- Repeat:

  ```
    // Cluster Assignment
    for i = 1 to m:
      c^(i) := index ( from 1 to K ) of Cluster Centroid closest to x^(i) // ||x^(i) - mu_k||
    
    // Move Centroid
    for k = 1 to K:
      mu_k := average ( mean ) of points asssigned to cluster k // A vector in R^n
  ```

  - In the code above
    
    - _$c^{(i)}$ means the index of cluster to which example $x^{(i)}$ is currently assigned._
    
    - _$\mu_k\  \text{means the cluster centroid}\  k (\mu_k \isin\R^n)$_
    
    - _$\mu_{c^{(i)}}$ means the cluster centroid of cluster to which example $x^{(i)}$ has been assigned._

#### Optimization Objective of K-Mean: Distortion Function

- $J(c^{(1)}, ..., c^{(m)}, \mu_1, ..., \mu_k) = \frac{1}{m}\sum_{i = 1}^m||x^{(i)} - \mu_{c^{(i)}}||^2$

#### Initialize K-Means

- Randomly pick K training examples

- Set $\mu_1, ..., \mu_k$ equal to these K examples.

  ```
    for i = 1 to 100{

      Randomly initialize K-means
      Run K-means, Get c^(1), ..., c^(m), mu^(1), ..., , mu^(K)
      Compute the distortion Function
    }

    Pick clustering that gave lowest distortion Function value.
  ```

#### Choosing the number of clusters

- Alternative: Draw the "K - Distortion Function Value" plot. ( Elbow Method )
  
  ![Elbow](/elbow.png)

## Dimentionality Reduction

### PAC: Principal Component Analysis

- Reduce from 2-dimension to 1-dimension: Find a direction ( a vector $\mu^{(1)} \isin \R^n$ ) onto which to project the data so as to minimize the projection error.

- Reduce from n-dimension to k-dimension: Find k vectors ( vectors $\mu^{(1)}, ..., \mu^{(k)}$ ) onto which to project the data, so as to minimize the projection error.

- Reduce memory / disk needed to store data

- Speed up learning algorithm

- __Bad use of PCA: To prevent overfitting. Instead, use regularization.__

- __PCA is not Linear Regression!__

  ![PCANlinear](/PCANlinear.png)

### Data Processing

- Training Set: $x^{(1)}, x^{(2)}, ..., x^{(m)}$

- Preprocessing ( Feature Scaling / Mean Normalization )
  
  $\mu_j = \frac{1}{m}\sum_{i = 1}^mx_j^{(i)}$

  Replace each $x_j^{(i)}$ with $x_j - \mu_j$

  If different features have different scales, scale Features to have comparable range of values $x_j \larr \frac{x_j^{(i)} - \mu_j}{s_j}$

### PCA algorithm

- Reduce data from n-dimensions to k-dimensions

- Compute "convariance matrix"

  $\Sigma = \frac{1}{m}\sum_{i = 1}^{m}(x^{(i)})(x^{(i)})^T, \Sigma \isin \R^{n\times n}$

- Compute the "eigenvectors" of $\Sigma$:
  
  ```
    [U, S, V] = svd( Sigma ) // Singular Value Decomposition;
    Uredece = U(:, 1:k);
    z = Ureduce' * x;  
  ```

  From the formular above we get:
    
    $U = \begin{bmatrix}|&|&...&|\\\\u^{(1)}&u^{(2)}&...&u^{(n)}\\\\|&|&...&|\end{bmatrix} \isin \R^{n\times n}$

  Then we use the first k columns in the Matrix:

    $z^{(i)} = U_{reduce}^Tx^{(i)} = \begin{bmatrix}|&|&...&|\\\\u^{(1)}&u^{(2)}&...&u^{(k)}\\\\|&|&...&|\end{bmatrix}^Tx^{(i)} = \begin{bmatrix}-&(u^{(1)})^T&-\\\\...&...&...\\\\-&(u^{(k)})^T&-\end{bmatrix}x^{(i)} \isin \R^{k\times 1}$

### Choosing k ( number of principle components )

- Average squaied projection error: $\frac{1}{m}\sum_{i = 1}^m||x^{(i)} - x_{approx}^{(i)}||^2$

- Total variation in the data: $\frac{1}{m}\sum_{i = 1}^{m}||x^{(i)}||^2$

- Typically, choose k to be smallest value so that:

  $\frac{\frac{1}{m}\sum_{i = 1}^m||x^{(i)} - x^{(i)}_{approx}||^2}{\frac{1}{m}\sum_{i = 1}^{m}||x^{(i)}||^2} \leq 0.01$

  "99% of variances is retained"

- __Algorithm:__

  - Try PCA with k = 1
  
  - Compute $U_{reduce}, z^{(1)}, z^{(2)}, ..., z^{(m)}, x_{approx}^{(1)}, ..., x^{(m)}_{approx}$
  
  - Check if $\frac{\frac{1}{m}\sum_{i = 1}^m||x^{(i)} - x^{(i)}_{approx}||^2}{\frac{1}{m}\sum_{i = 1}^{m}||x^{(i)}||^2} \leq 0.01$

    `[U, S, V] = svd( Sigma )`

    For given k, $\frac{\frac{1}{m}\sum_{i = 1}^m||x^{(i)} - x^{(i)}_{approx}||^2}{\frac{1}{m}\sum_{i = 1}^{m}||x^{(i)}||^2} = 1 - \frac{\sum_{i = 1}^ks_{ii}}{\sum_{i = 1}^{n}s_{ii}} \rarr \frac{\sum_{i = 1}^ks_{ii}}{\sum_{i = 1}^{n}s_{ii}} \geq 0.99$

  - Pick k, that satisfies $\frac{\sum_{i = 1}^ks_{ii}}{\sum_{i = 1}^{n}s_{ii}} \geq 0.99$

### Reconstruction from compressed representation

- $X_{approx} = U_{reduce} \times z$

### Design of ML system with PCA

- Get Training Set

- Run PCA to reduce $x^{(i)}$ in dimension to get $z^{(i)}$

- Train logistic regression on $\{(z^{(1)}, y^{(1)}), ..., (z^{(m)}, y^{(m)})\}$

- Test on test set: Map $x_{test}^{(i)}\ \text{to}\ z_{test}^{(i)}$. Run $h_\theta(z)$ on $\{(z_{test}^{(1)}, y_{test}^{(1)}), ..., (z_{test}^{(m)}, y_{test}^{(m)})\}$

- Before implementing PCA, first try running whatever you want to do with original / raw data $x^{(i)}$. Only if that doesn't do what you want, then implement PCA and consider using $z^{(i)}$

## Anomoly Detection

### Example: Fraud Detection

- $x^{(i)}$ = features of user i's activities

- Model $p(x)$ from data

- Identify unusual users by checking which have $p(x) < \epsilon$

### Gaussian Distribution

- Say $x \isin \R$. If x is a disatributed Gaussian with mean $\mu$, variance $\sigma^2$.

- $p(x; \mu, \sigma^2) = \frac{1}{\sqrt{2\pi}\sigma}exp^{(-\frac{(x - \mu)^2}{2\sigma^2})}$. Here $\sigma$ is the standard deviation.

  ![Gaussian](/Gaussian.svg)

- As for "Parameter estimation"...
  
  - $\mu = \frac{1}{m}\sum_{i = 1}^mx^{(i)}$
  - $\sigma^2 = \frac{1}{m}\sum_{i = 1}^m(x^{(i)} - \mu)^2$

### Algorithm

- Training Set $\{x^{(1)}, ..., x^{(m)}\}$
  
- Each Example is $x \isin \R^n$

1. Chosse features $x_i$ that you think might be indicative of anomalous examples.

2. Fit parameters $\mu_1, ..., \mu_n, \sigma_1^2, ..., \sigma_n^2$

    $\mu = \frac{1}{m}\sum_{i = 1}^mx^{(i)}$
  
    $\sigma^2 = \frac{1}{m}\sum_{i = 1}^m(x^{(i)} - \mu)^2$

3. Given new example x, compute $p(x)$

    $p(x) = \prod_{j = 1}^np(x_j;\mu_j, \sigma_j^2) = \prod_{j = 1}^n\frac{1}{\sqrt{2\pi}\sigma}exp^{(-\frac{(x - \mu)^2}{2\sigma^2})}$

  Anomaly if $p(x) < \epsilon$

#### Evaluation

- Fit model $p(x)$ on training set $\{x^{(1)}, ..., x^{(m)}\}$

- On a Cross Validation / Test example, predict

  $y = \begin{cases}1,\ p(x) < \epsilon\ \text{(anomaly)}\\\\0,\ p(x) \geq \epsilon\ \text{(normal)}\end{cases}$

- Possible evaluation metrics:
  
  - True positive, false positive, false negative, true negative
  
  - Precision / Recall
  
  - F-Score

  Can also use the Cross Validation Set to choose parameter $\epsilon$

### Anomoly Detection vs. Supervised Learning

|Anomoly Detection|Supervised Learning|
|:---------------:|:-----------------:|
|Very small number of positiv examples but large number of negative examples|Large number of positive and negative  examples|
|Many different types of anomalies. Hard for any algorithm to learn from positive examples what the anomalies looks like|Enough positive examples for algorithm to get a sense of what positive examples are like|
|Future anomalies may look nothing like any of the anomalous examples we've seen so far|Future positive examples likely to be similar to ones in training set|

### Error Analysis for anomaly detection

- Want $p(x)$ large for normal examples x
    
    $p(x)$ small for anomalous examples x

- Most commen Problem:
    
    $p(x)$ is comparable ( say, both large ) for normal and anomalous examples.

### Multivariance Gaussian Distribution

- $x \isin \R^n$, don't model $p(x_1), p(x_2)$, ..., etc. separately. Instead, model $p(x)$ all in one go.
- Parameters: $\mu\isin\R^n, \Sigma \isin \R^{n\times n}$, the "convariance matrix"
