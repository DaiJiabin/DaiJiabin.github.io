# Machine Learning


# Lecture by [Andrew Ng, Coursera](https://www.coursera.org/learn/machine-learning)

## Week 1

### Supervised Learning vs. Unsupervised Learning

- Supervised Learning: 

  > In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.
  
  - Training Data already has the value, which our Function should predict for a new, strange input. i.e, In the case below, we want to get a function, so that we can calculate the price of a house to be sold. We have __4 Training Data__ in this table and each Data has 4 __Features__ that have a influence on its' price ( we call it as __Multi-Features__. It'll be discussed later:) ).

  - It's devided in __Regression__ and __Classification__ Problems
  

||Size($m^2$)|Number of Bedrooms|Number of Floors|Age(years)|Price(1000$)|
|:---:|:---------:|:----------------:|:--------------:|:--------:|:---:|
|($TrainingData_1$)|2104|5|1|45|460|
|($TrainingData_2$)|1416|3|2|40|232|
|($TrainingData_3$)|1534|3|2|30|315|
|($TrainingData_4$)|852|2|1|36|178|
|...|...|...|...|...|...|
||($x_1$)|($x_2$)|($x_3$)|($x_4$)|($x_5$)|

- Unsupervised Learning 
  
  > Unsupervised learning, on the other hand, allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

### Regression vs. Classification

- Regression: The Value we want to predict is __continous__ instead of discrete. i.g., the Price of a House.

    > In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function. 

- Classification: As its' name, we want to __devide the input in different classes__. i.g., After training, with the help of the <u>color, weight, outlook and smel</u> ( __Features__ ), we want to predict if the coffee beans we have come from Arabica or Robusta.

    > In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories.

### Linear Regression with 1 Variable / Feature

- Hypothesis Function
  - $\hat y = h_\theta = \theta_0 + \theta_1x$
- Cost Function
  - $J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^m(\hat y_i - y_i)^2 = \frac{1}{2m} \sum_{i=1}^m(h_\theta(x_i) - y_i)^2$
- Optimize
  - __Gradient Descnet.__ More specifically, repeat:
  
    $tmp_0 = \theta_0 - \alpha\frac{\partial}{\theta_0}{J(\theta_0, \theta_1)} = \theta_0 - \alpha\frac{1}{m}\sum_{i=1}^nm{(h_\theta(x_i) - y_i)}$
    $tmp_1 = \theta_1 - \alpha\frac{\partial}{\theta_1}{J(\theta_0, \theta_1)} = \theta_1 - \alpha\frac{1}{m}\sum_{i=1}^m{((h_\theta(x_i) - y_i)x_i)}$
    $\theta_0 = tmp_0$
    $\theta_1 = tmp_1$

    We call $\alpha$ __Learning Rate.__ Its' value has influence on the speed, how fast we can find the parameters, with that we can reach a local optimal value.
  - __When $\alpha$ too large / too small is:__
    - too large: we might miss the parameters, which can help us get the local optimal value.
    - too small: We need more iterations ( Baby Steps / more time ).
    - We can make the judge, whether $\alpha$ too large / small ist by drawing the plot of __iterations - $J(\theta_0, \theta_1)$:__ It should be lower. Otherwise is $\alpha$ too large.
    - We can start $\alpha$ from __0.001, ..., 0.01, ..., 0.1.__ And Andrew Ng advises us to use 3 times ( 0.001, 0.003, 0.01, 0.03, 0.1 ) to try it.
