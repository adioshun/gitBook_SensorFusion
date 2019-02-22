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
- [conditional distributions](https://github.com/adioshun/gitBook_Statistics/blob/master/probability/probability-function/conditional-distribution.md)
- [joint distributions](https://github.com/adioshun/gitBook_Statistics/blob/master/probability/probability-function/joint-distribution-function.md)

isolated distribution of a single random variable, where we have removed the influence of all the other variables.
- [marginal distribution](https://legacy.gitbook.com/book/adioshun/statics-with-r/edit#/edit/master/probability/probability-function/joint-distribution-function.md?_k=u75e4h)

### [1.4.3 Expectations, covariance and the Gaussian distribution]((https://github.com/adioshun/gitBook_Statistics/blob/probability/probability-distribution/meanvector-covariancematrix.md)


> 1.4 Expectation Covariance Gaussian MED INTRO V3-en


our goal is to describe our results using 
- the mean vector or expected value 
- the covariance matrix of a Gaussian distribution.

And if our result is not Gaussian, we anyway tend to approximate our results using the mean and covariance of this non-Gaussian distribution,even though these do not fully capture all the facets of our actual distribution.

So as we said, probability distributions are also characterized by their mean vectors and covariance matrices.

So how do we calculate this?Well, the expected value or mean of an m-dimensional randomvector x, defined like this, is the expected value of x.
Now, the expectation of x is definedas an integral of the vector x weighted by the probabilitydensity of that vector.
So what we have here is that for valuesof x which have high probability densitywill influence our expected valuemore than values of x which have low probability density.
Often we denote this mean vector here as either mu, or x barin this case.
And we call this the first moment of p of x.
Now, the notation here is simply shorthand that weintegrated from minus infinity to infinityfor all the dimensions of x.
So that was the expected value.
Now, the covariance of x or the second central momentof p of x is written like this and is definedas the expectation of x minus its mean times the same thingtransposed.
Now, we can view this factor hereas the distance between x and its mean,that is, how much does x spread around its mean value?Now, if we write it like this, weassume that x is a column vector,as we will do throughout the whole of this course,as this here, the product here, should be an outer product.
That is, we have a tall matrix times a wide matrix.
So this product here is an m by m squared matrix, whichis symmetric and positive semidefinite, as thisis a square here.
So it needs to be positive semidefinite.
So that is the definition of the covariance matrixof a random variable x.
Now, for discrete-valued random variables,the above integrals are then replacedby corresponding summations.
So we have summation here instead.
So let us look a bit more into howwe can interpret this covariance matrix using an example wherewe have independent samples from a zero-mean two-dimensionalrandom vector x, which has the components x1 and x2.
Now, our samples are plotted in red here in this figure.
The question is if you can guess the covariance matrixof x using these samples here.
Now, to help you out a bit, we have alsoplotted to one standard deviationand three standard deviation contoursof the distribution of x.
So we have three sigma contour here,and we have one sigma contour here.
Additionally, we can mention that the covarianceof a two-dimensional random variablehas the following structure.
So the covariance of x can be written like this, wheresigma 1 is the standard deviation of x1 and sigma 2is the standard deviation of x2.
And the factor rho here is what'scalled a correlation factor.
So what do you think the covariance of x is?I would encourage you to pause the video here and thinkabout this yourself for a couple of minutes.
And then we can go through the results together.
So as I mentioned, the covariance matrixis a measure for how the samples of a random vectorhave spread around its mean.
Now, as x is a zero-mean random vector,its mean is located here at 0, 0.
And if we look at the structure of the covariance matrixthat we'll find here, we see that we basicallyneed to find the standard deviation of x1 and x2plus the correlation factor rho.
Now, the standard deviation of x1 and x2can be found by projecting this one sigmacontour onto both dimensions here and thenlooking at the distance between the projectedcontour and the mean.
So if we do this, we get sigma 1 and sigma 2approximately equal to 1.
4.
So we can start filling in our covariance matrix here.
So what about the correlation factor?So we know that the correlation factoris a value between minus 1 and 1 that tells us how correlatedtwo random variables are.
If the correlation factor is, for example, 1,the two random variables are fully positively correlated,meaning that x1 here, for example,is a deterministic positive function of x2, and vice versa.
Now, if we look at our samples, wesee that there is quite a significant positivecorrelation here.
So if we have a high value on x1,there's a high probability that x2 also has a high value.
But it's definitely not a deterministic mapping, right,as if it were, all the samples here would collapse and fallon the line like this.
But that's not the case, right?So we have some spread around us.
So this would mean rho equal to 1,if all the samples were on this line.
Now in this case, I would say that the correlationis somewhere around 0.
9.
So we have 0.
9 here.
Putting this together, we get a final guessfor our covariance matrix, which is--so the variance in each dimension is around 2.
And we have a cross-covariance of 1.
8.
So does this match what you guessed?So if we look at the covariance matrix for a random variable,it will tell us both the variancein the different dimensions, but it will alsotell us how correlated the different dimensions are.
So we have a cross-covariance of 1.
8 here between x1 and x2.
And this information is somethingthat is used extensively in sensor fusion and nonlinearfiltering, which we will see later in this course.
Sometimes we're interested in findingthe expected value of a random variable numerically.
Perhaps we are not able to solve the involved integralsexplicitly, or more commonly, when we do not actuallyknow the underlying distribution but have accessto a large number of samples from it.
So in this case, we can use the law of large numbers, whichstates that sample averages convergeto expected values for large sample sizes.
Now, if x1, x2, and so on are independent and identicallydistributed random variables, distributed accordingto some distribution p of x, then the sample average,that is, we sum all the samples and divideby the number of samples, will convergeto the actual expected value of xunder p of x if we let the number of samplesgrow to infinity.
Now, we can think of this as throwing a dice many times,where each roll of the dice would generatea new, independent, and identically distributedsample from a distribution of dice face values.
If we do this sufficiently many times,eventually the average face valueconverges to expected value, which we cancalculate to be 3.
5, like this.
So this is a way to numerically calculate expected values.
So now that we know what the expected value and covarianceis, it's time to look at the most important distributionof them all, at least in this course.
And that is the Gaussian distribution.
And as you will see, there is a clear connectionwith the mean and covariance of a random variable.
So we write like this to denote that xis a Gaussian random variable with mean mu and covariance Q.
And the pdf of x is then denoted like this, so pof x where we use this notation here to denote the Gaussianpdf as a function of x with the parameters mu and Q.
Note that there's a important difference with whatwe write here, where we are saying that x is distributedaccording to Gaussian distributionwith these parameters, mu and Q.
 
But here we are referringto the actual function as a function of xwith these parameters.
So by definition, the Gaussian pdfcan be expressed like this, wherewe have here a constant term, whichis dependent on the covariance, times the exponentialto the power of a quadratic function of x.
We will have x minus its mean squared, whichis then normalized by or scaled by the covariance matrixinverse.
If we plot this function here in the scalar case for a Gaussiandistribution with mean 0 and variance 1,we get this classical bell-shaped curve,where the peak is at the mean, which is 0 in this case,and the spread around the mean is dependent on the variance.
So note that a Gaussian random variable is completelydetermined by its mean and its covariance matrix.
So we do not need any other parameters to describea Gaussian distribution.
Later in this course, we will use this extensivelywhen we describe the results of our filters.
One of the nicer properties with Gaussian random variablesis what happens when we have a linear combinationof independent Gaussian random variables.
So let x and y be Gaussian random variableswith these means and covariances.
If we now construct a new random variablez, which is then a linear combination of x and ylike this, so z is equal to A timesx plus B times y, where A and B are now deterministic matrices.
Then z will also be a Gaussian random variable, which meancan be calculated like this.
So the mean of z is the expected value of Ax plus By.
Now, as we can always split the expectation of a suminto its individual components, we get the expected value of Axplus the expected value of By.
And A and B are deterministic matrices,we can move them outside of the expectations.
So we get A times the expected valueof x, which is mu x, plus B times the expected value of y,which is mu y.
Now for the covariance, it's a bit more tricky.
But by definition, the covariance of zis equal to the covariance of Ax plus By.
We just insert what z is, right?Now, as x and y are independent, wecan divide this covariance of this suminto the covariance of the different parts hereor the different terms in the sum.
Now, note that we cannot do this in general,as we need to consider the cross-covariance terms,which in this case is the cross-covariance of Ax,By and the cross-covariance of By and Ax.
But as x and y are independent, these terms here are 0.
So we can ignore them here.
Now again, as A and B are deterministic,we can move them outside of the covariance.
But instead of getting them just as a factorthat we got here when we calculated the mean,we get them squared here.
And as we're dealing with matrices,we need to be a bit careful about which orderwe do the square.
So in this case, we get A times Qx, A transpose,plus BQy, B transpose.
And this is a general rule for the covariance.
So if you have a covariance of deterministic matricestimes a random vector, the resultwill be A times the covariance of the random vectortimes A transpose.
Now, if you feel that I went through this a bit quickly,I would highly recommend that youtry to derive this expression here yourselfusing the definition of covariancethat we presented at the beginning of this lectureand perhaps also brush up on rules relatedto the expectation operator.
And I will think that you will find this well worth the effortwhen we start to discuss the actual material of this course.
For your convenience, here is a summary of the basic statisticsresult that we have presented in this set of primerin statistics lectures.
I would encourage you to familiarize yourselfwith these expressions and make sure that youunderstand what they are.
You might also find this slide handywhen we go through the results about nonlinearfiltering and the rest of the lectures in this course.



### 1.4.4. Exercises

![](https://i.imgur.com/HAN0Cd3.png)

![](https://i.imgur.com/OfzRTVN.png)

