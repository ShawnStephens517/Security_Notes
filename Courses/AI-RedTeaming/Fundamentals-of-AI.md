# Fundamentals of AI
This is a module from HTB Academy's AI Red-Teamer Path

## Intro to ML
### AI
    - NLP (Natural Language Processing) - Think ChatGPT, Claude, Gemini
    
    - Computer Vision - Think Python video/image analysis
    
    - Robotics
    
    - Expert Systems - Decision making. Advanced Reasoning. AGI

#### Machine Learning
    - Supervised Learning - Spam Detect, Image Class, etc... Requires labeling/outcome matching
    
    - Unsupervised - Anomaly. Doesn't require outcome prior to classifications
    
    - Reinforcement - Trial and Error

#### Deep Learning
    - Hierarchical Feature Learning - Multilayer learning. Detect shades of color, and then detect shapes
    
    - E2E - Map data to outputs without manual engineering

    - Scalability - Big Data

    - Neural Nets in DL
        - Convolutional NN (CNN) - Image and Video
        
        - Recurrent NN (RNN) - Sequential Data, Text & Speech. Loops allow perisistance across steps

        - Transformers - self-attention for long-range dependencies
---
---
## Math Refresh

### Common Python Math Operators
```python
* = Multiplication

/ = Division

+ = Addition

- = Subtraction

x_t = Subscript (time series data)

x^2 = SuperScript (exponent, to the power of)

||x|| = Norm (Measure size/distance of vector)

Σ = Summation (mean, variance, series)

log2(x) = Used to measure entropy

ln(x) = Natural logarithm. Calculus, differential, probability

e^x = Exponent used for growth and decay. Math and Physics

2^x = Used in Binary Representation (CS). Base 2

A * V = Matrix-Vector. Linear Algebra ((X)NN)

A * B = Matrix-Matrix. Linear transformations. Linear Algebra (DL layers)

A^T = Transpose. Swaps Row and Columns.

A^{-1} = Inverse. Linear Algebra

det(A) = Determinant matrix. Square. Volume, area, geometry

tr(A) = Trace. Square Matrix. Sum of main diagonal.

|s| = Cardinality. Counting, probability, combinations

u = Concat. Data Merge

n = Intersection. Common elements, filtering.

A^c = Complement. Set of elements not in defined variable(A). probability.

>= = Greater than or Equal

<= = Less than or Equal

== = Equality

!= = Inequality

λ = Lambdas. Linear Transform, optimization

A * v = λ * v = Eigenvector. Maximum variance. - Need More Research ??

max(x,x,x) = largest value from set. Best Solution. Decision-making

min(x,x,x) = smallest value.

1 / x,x,x = Invert value. Rates & proportions

... = Ellipsis. Continuation of sequence. 

f(x) = Function Notation. Math relationship

P(Out | Input) = Conditional Probability. Bayesian, decision-make, probability

E[X] = Expectation. Mean. decision-making, statistics

Var(x) = Variance. Risk Assessment.

σ(X) = Standard Deviation. assess risk. sqrt(Var(X))

Cov(X, Y) = Covariance. Relationship between 2 vars, statistics

ρ(X, Y) = Correlation. Statistics, relationship between variables.
```

---
---

## Supervised Learning Algos
### Core Concepts
- 2 main categories
    - Classification = goal is prediction category labels. Spam class
    - Regression = goal is prediction continous values. Stock Market
- Training Data = Consists of input features and output labels
    - EX: Sample math problems with correct solution

- Features = measurable properties serves as input to models
    - EX: Housing prices. SQFT,#Rooms, Age, Geo

- Labels = Known Outcomes.
    - EX: Actual Home Price

- Model = Takes input features and outputs labels
    - Used to predict unseen data. 

- Training = Process of feeding data to algos. Iterative adjustments

- Predictions = Once trained, predicts labels(output) from new features(input)

- Inference = Focus on interpreting vs determining actionable results(labels). Insights, relationships between features(input)

- Evaluation = analyze model performance
    - Accuracy = Correct labels
    - Precision = true positive vs all positive predictions
    - Recall = true positive vs all actual positive
    - F1-Score = blance measure between precision & recall

- Generalization = Ability to predict outcomes(labels)

- Overfitting = Over learns the data vs the underlying pattern

- Underfitting = Model to simple to determine underlying patterns

- Cross-Validation = Generalization testing. Split data into subsets and train on different subset combinations.

- Regularization = Adds penalty term to loss function.
    - L1 = Penalty to absolute value of coefficients
    - L2 = Penalty to square of coefficients
---

## Linear Regression
### Core Concepts
Regression is analysis where goal is predicting target variable.

In a graph, this is the line that cuts through the median of the output values. A good example to utilize this concept is using a trading platform's trading tools to analyze past performance and predict possible movement.

**Examples**
    
    - Predict house prices
    - Forcast weather/temprature
    - Web Trafic predictions

#### Ordinary Least Squares(OLS)
---
Method for estimate optimal values in coefficients. Minimize sum of squared differences between actual and predicted values

**OLS Process**
- Calculate Residual = difference between actual *y* and predicted *y*
- Square Residuals = Ensures positive values and larger weight to errors
- Sum the Squared (RSS) = Deduced to a single sum value representing overall erro.
- Minimize RSS = adjusts coefficients to find result in smallest RSS

#### Assumptions
---
- Linearity = relationship exists predictor and target
- Independence = observations are independent of each other
- Homoscedasticity = variance of errors constant. Spread of residuals roughly the same
- Normality = normally distributed errors. Important for valid inferences

#### Simple Regression
---
Uses 1 predictor var and 1 target var. HTB example
```python
y = mx + c

Where:

y is the predicted target variable
x is the predictor variable
m is the slope of the line (representing the relationship between x and y)
c is the y-intercept (the value of y when x is 0)
```
Trying to find optimal values for *m* & *c*

used with Ordinary Least Squares. Minimizing sum of square errors.

#### Multiple Regression
---
Multiple vars. HTB example
```python
y = b0 + b1x1 + b2x2 + ... + bnxn

Where:

y is the predicted target variable
x1, x2, ..., xn are the predictor variables
b0 is the y-intercept
b1, b2, ..., bn are the coefficients representing the relationship between each predictor variable and the target variable.
```

## Logistic Regression
### Core Concepts

#### Assumptions
---
- Binary Outcome = Target Var categorical, only 2 outcomes
- Linearity of Log Odds = Log odds are transform of probability. Probability of event divided by probability of not occuring
- No/Little Multicollinearity = Multicollinearity is highly correlated predictor var, hurts determining individual effects
- Large Sample Sizes = Larger datasets ideal. Better performance.

#### Classification
---
Assigns data points to category or classes. Predicts discrete labels
- Identify fraud charges
- Classify animal
- Diag disease based on patient symptoms

#### How Logistic Regression Works
---
Outputs probability between 0 & 1. Likelihood of input to category

**Sigmoid function** maps  input to a value 0 to 1 range. Allows model to capture complex relationships between input and output. ***S*** Shaped graph

HTB Example
```python
P(x) = 1 / (1 + e^-z)

Where:

- P(x) is the predicted probability.
- e is the base of the natural logarithm (approximately 2.718).
- z is the linear combination of input features and their weights, similar to the linear regression equation: z = m1x1 + m2x2 + ... + mnxn + c
```

In logistic regression, the line is the decision boundary. Used to determine which class the input falls into.

**Hyperplane**
- Simple line in 2D space (two regions)
- Flat plane in 3D space divides the space into 2 halves
- Defined by models coefficients (learned parameters).

#### Threshold Probability
---
Usually set to 0.5 but adjustable to find the desired balance true/false positives.

P(x) Above threshold, positive else negative class

## Decision Trees
### Core Concepts
Used in classification and regression. Easier to understand.

**3 Main components**
- Root Node = Starting Point
- Internal Nodes = Branches of decision rules
- Leaf Nodes = Terminal nodes. Final outcome/prediction

### Building a Decision Tree
#### Gini Impurity
HTB Example:
```python
Gini(S) = 1 - Σ (pi)^2

Where:

    S is the dataset.
    pi is the proportion of elements belonging to class i in the set.

Consider a dataset S with two classes: A and B. Suppose there are 30 instances of class A and 20 instances of class B in the dataset.

    Proportion of class A: pA = 30 / (30 + 20) = 0.6
    Proportion of class B: pB = 20 / (30 + 20) = 0.4


The Gini impurity for this dataset is:


Gini(S) = 1 - (0.6^2 + 0.4^2) = 1 - (0.36 + 0.16) = 1 - 0.52 = 0.48

```

#### Entropy
---
Measures disorder within a set.

HTB Example
```python
Entropy(S) = - Σ pi * log2(pi)
Where:

S is the dataset.
pi is the proportion of elements belonging to class i in the set.
Using the same dataset S with 30 instances of class A and 20 instances of class B:

Proportion of class A: pA = 0.6
Proportion of class B: pB = 0.4
```

```python
Entropy(S) = - (0.6 * log2(0.6) + 0.4 * log2(0.4))
           = - (0.6 * (-0.73697) + 0.4 * (-1.32193))
           = - (-0.442182 - 0.528772)
           = 0.970954
```


#### Information Gain
---
Measures reduction of entropy by splitting a set.
```python
Information Gain(S, A) = Entropy(S) - Σ ((|Sv| / |S|) * Entropy(Sv))


Where:

S is the dataset.
A is the feature used for splitting.
Sv is the subset of S for which feature A has value v.
```

#### Putting it together (Building the tree)
---
