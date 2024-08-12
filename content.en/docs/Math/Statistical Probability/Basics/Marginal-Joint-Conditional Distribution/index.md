---
title: Marginal/Joint/Conditional Distribution
---
To better understand the concepts of **joint distribution**, **conditional distribution**, and **marginal distribution**, we will go through each concept in detail along with illustrative examples.

### **1. Joint Distribution**

**Joint distribution** describes the probability of two or more variables occurring simultaneously. In other words, it tells us the probability of a set of variables happening together.

#### **Formula**:
- For two random variables \(X\) and \(Y\), the joint distribution is denoted as \(P(X = x, Y = y)\), representing the probability that \(X\) takes value \(x\) and \(Y\) takes value \(y\) at the same time.

#### **Example**:
- Suppose you are interested in the probability that a student receives an A grade in both Math and Literature.
  - Let \(X\) be the Math grade and \(Y\) be the Literature grade.
  - The joint distribution will tell you the probability that a student receives an A in both Math and Literature, for example, \(P(X = A, Y = A)\).

### **2. Conditional Distribution**

**Conditional distribution** describes the probability of a variable occurring given that another variable is known. It allows us to calculate the probability of one event based on known information about another event.

#### **Formula**:
- The conditional distribution of \(Y\) given \(X\) is denoted as \(P(Y = y | X = x)\), representing the probability that \(Y\) takes value \(y\) given that \(X\) has taken value \(x\).

#### **Example**:
- Continuing with the previous example, suppose you know that a student received an A in Math. Now, you want to know the probability that the same student also received an A in Literature.
  - This is expressed by the conditional distribution: \(P(Y = A | X = A)\).

### **3. Marginal Distribution**

**Marginal distribution** describes the probability of a single variable without considering the other variables. This is the distribution of one variable when we "marginalize" or "sum out" the other variables.

#### **Formula**:
- The marginal distribution of \(X\) is denoted as \(P(X = x)\), and it is calculated by summing (or integrating) the values of the joint distribution over all possible values of the other variable, for example, \(Y\):
  \[
  P(X = x) = \sum_y P(X = x, Y = y)
  \]

#### **Example**:
- If you are only interested in the probability that a student receives an A in Math, without considering the Literature grade, the marginal distribution will provide this information.
  - For example, \(P(X = A)\) gives you the probability that a student receives an A in Math, regardless of the Literature grade.

### **Illustration with a Hypothetical Data Table**

Suppose you have a data table about students' grades in two subjects, Math (X) and Literature (Y):

| Math (X) | Literature (Y) | Number of Students |
|----------|----------------|-------------------|
| A        | A              | 10                |
| A        | B              | 20                |
| B        | A              | 15                |
| B        | B              | 5                 |

#### **Joint Distribution**:
- \(P(X = A, Y = A)\) = Probability that a student receives an A in both Math and Literature = \( \frac{10}{50} = 0.2\).

#### **Conditional Distribution**:
- \(P(Y = A | X = A)\) = Probability that a student receives an A in Literature given that they received an A in Math = \( \frac{10}{30} = 0.33\).

#### **Marginal Distribution**:
- \(P(X = A)\) = Probability that a student receives an A in Math, regardless of the Literature grade = \( \frac{10 + 20}{50} = 0.6\).

### **Conclusion**
The three concepts **joint distribution, conditional distribution, and marginal distribution** provide different ways to describe and calculate the probabilities of random variables in statistics and machine learning. These concepts form the foundation for many algorithms and methods in data processing and machine learning.