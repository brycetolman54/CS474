# Loss functions

- We are assuming that we have a set of inputs and outputs that we are trying to learn the relation between
    - $\{x_i,y_i\}^{I}_{i=1}$
    - This could be us predicting some regression or some classification (among other things)

- We need to know how well our model is doing, so we need a loss function to tell us how far we are off from what we want
    - $L[\phi]$ -> gives a scalar output that is lower when we are closer to the right prediction
- Types of predictions:
    - Regression (give a real, arbitrary value)
    - Binary Classification (give a single class to belong to out of two classes)
    - Multi-class classification (give a single class to belong to out of an arbitrary number of classes)
    - Multi-label classification (give multiple labels for the input)
- In this class, we are going to try to model our data as a distribution, so we have to think about the distribution we are looking for in each case
    - This could be Gaussian, Bernoulli, Multi-class distribution, etc.
- The problem with modeling regression with just a line for real-world data is that we don't get probability distributions
    - We know that there is not one height for all people one age (For example), so a line, which assumes that there is, is not great
        - We need to predict distributions rather than just a line, how can we do that?
- We are going to make a model that predicts probability of $y$ given inputs $x$
- We use $\theta$ to represent the parameters of the distribution that we are predicting (separate from the $\Omega$ which represents the parameters for the actual model)
- Once we have predicted a distribution, we have to decide what the actual answer is
    - Maybe we want the whole distribution
    - Maybe we just want the max of the function (the mean for a Gaussian)
    - We could also randomly (??) sample the distribution to get a guess and our confidence in it
- The <b>Maximum Likelihood Criterion</b>
    - We want to maximize the product of distributions (We want high probabilities) of the output given each input
    - When we consider this probability in terms of $\phi$, we call it the likelihood
    - We are assuming that our data is <i>iid</i>, identically and independently distributed
        - The probabilities must all come from the same distribution (i.e. that all are Gaussian) -> That is the identical
        - The model for $i$ doesn't depend on $i + 1$ or $i - 1$ (i.e that no coin flip affects another) -> That is the independent (it allows us to do the product)
- <b>A problem</b>: multiplying probabilities makes it really hard to keep track of them with finite precision
    - So, we do $log()$ on the product to turn it into sums
        - This makes it much easier to keep track of things with precision
    - The $log$ is monotonically increasing, it never goes down
        - This means the max or min of our functions never change (the absolute value does, but the relative difference)
    - This becomes what we call the <b>Maximum Log Likelihood</b>
- From there, we just flip it, multiplying it by -1, and now finding the minimum of our function. :)
    - All training is is to find this minimum of the Loss function
        - You could do a brute force search, but that is dumb, so we have better ways to do it

- Recipe for Loss Functions
    1. Pick a probability distribution that matches what you are trying to predict
    2. Set the machine learning model to predict the parameters of that distribution
    3. Train the model to find those probability parameters that make the loss at a minimum
    4. Perform inference with the output distribution to get your final answer

- Examples:
    - Univariate regression: 
        - We choose a normal distribution, because that makes sense
        - Our network, then, needs to spit out the mean (we are ignoring variance, assuming it is constant)
        - So, we train to find parameters for the network that minimize the log likelihood
            - Fun fact, we make some simplifying moves that make this log loss end up as least squares
            - That means that least squares is measuring (as we want) the probability distribution for our points
            - In linear regression, we can think of just wanting the mean (the actual point), not the spread
                - The spread does tell us about our confidence... :)
        - To do inference, just take the max of the distribution (or if you are just outputting a mean, that is it)
    - Binary classification:
        - We choose a Bernoulli distribution (this has the parameter $\lambda$, that is the distribution parameter we are predicting)
        - Our network needs to predict $\lambda$, but it can output any number...
            - So, we use a `sigmoid` to force it into this space
        - We do some log things, and we get binary cross-entropy loss
            - This is the function we use to train now :)
        - For inference: if the $\lambda$ is greater than 0.5, you classify as one, else 0
    - Multi-class classification:
        - We choose to use the categorical distribution
            - all variables have to add to 1, we have `K` variables
        - We need to predict $\lambda_K$
            - we can output any number, so... we use softmax to get the probability of K
            - $softmax_k[z]=\frac{e^{z_K}}{\sum_{i=1}^{K} e^{z_i}}$
            - The `z` is the output for a specific class
        - We find the network parameters in order to get $z_K$ biggest for what the class should be
        - we infer by grabbing the output `K` that has the highest probability
- Cross Entropy:
    - Tells us how different two distributions are
    - We care about the right answer (probability distribution) and the one we output
    - We can use Kullback-Leibler divergence to find the difference between the two probabilities
    - You can think of entropy in terms of how spread out the distribution probability is among the different classes that you can choose
    - We are trying to get our model to give a distribution that is as least different from the target distribution as we can
