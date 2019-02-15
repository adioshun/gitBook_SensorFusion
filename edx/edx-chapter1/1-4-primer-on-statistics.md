## 1.4 Primer in statistics

### 1.4.1 Random variables(확률 변수)

> 1.2 Random Variables MED INTRO V2-en



When we do nonlinear filtering,
- we need them to **describe the quantity** that we're interested in, for example, the position of a vehicle.
- We also need random variables to **describe the observations** that we want to filter.

To describe our random variables, we'd use the
- so-called probability mass function(PMF) for discrete-valued random variables and a
- so-called probability density function(PDF) for continuous valued random variables.

![](https://i.imgur.com/xNejMqE.png)

표기법 : Now, the probability mass function of a discrete-valued random variable is, in this course, denoted as Pr of z, or just P of z.
- Note also that we are using braces here to indicate that z is a discrete-valued random variable.

Now, our probability mass function need to have the following properties in order to be proper probability mass functions.

- 특징 #1 : First, the probability that our discrete-valued random variable z is equal to some integral value i, which is written like this, needs
to be greater than or equal to 0.
- Now, one way to view this value here is if we collect many values of z, the fraction of these that are equal to i is given by this number here.
- And this needs to hold for all values of i.

- 특징 #2 : The second property of our probability mass function is that if we sum over all values of z, this sum needs to be 1.
- That is, the probability that z takes any value needs to be 1.
- We can also note that as a consequence of these two, we cannot have a probability mass for a value i that is greater than 1, which seems to be reasonable, right?

예 : Now if we look at this use in the example of a fair dice, the probability mass function for the face value that I would get if we rolled the dice can
be written like this.
- So the dice has six faces with a value 1 through 6, which each is equally probable.
- So the probability that z is i is equal to 1/6, if i is equal to 1, 2, and so on up to 6, and 0 otherwise.
- If we visualize this pmf, it will look something like this, where we only have probability mass for discrete values.


![](https://i.imgur.com/6iENBYV.png)

### 1.4.2 Conditional, joint and marginal distributions

> 1.3 Distributions MED INTRO V3-en

how the distribution of two or more random variables depend on each other.
- [conditional distributions](https://legacy.gitbook.com/book/adioshun/statics-with-r/edit#/edit/master/probability/probability-function/conditional-distribution.md?_k=haw4u7)
- [joint distributions](https://legacy.gitbook.com/book/adioshun/statics-with-r/edit#/edit/master/probability/probability-function/joint-distribution-function.md?_k=u75e4h)

isolated distribution of a single random variable, where we have removed the influence of all the other variables.
- [marginal distribution](https://legacy.gitbook.com/book/adioshun/statics-with-r/edit#/edit/master/probability/probability-function/joint-distribution-function.md?_k=u75e4h)

### 1.4.3 Expectations, covariance and the Gaussian distribution

> 1.4 Expectation Covariance Gaussian MED INTRO V3-en




### 1.4.4. Exercises

![](https://i.imgur.com/HAN0Cd3.png)

![](https://i.imgur.com/OfzRTVN.png)

