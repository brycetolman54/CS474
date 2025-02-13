# Training models

- The idea is that we want to find the minimum
- In order to do this, we have to take a derivative of the loss (we want to get to the bottom of the loss) with respect to each of our parameters
    - These are partial derivatives
    - We then take a linear combination of all the parameters to find the actual way that we should go
        - In reality, I think we just move each parameter according to its gradient and that ends up moving us in their combined way down the slope

- If we just have a constant $\alpha$ (the learning rate), we can end up oscillating instead of just settling in the bottom
- Note to remember: we take the path of steepest descent, not the one that takes us most directly to the lowest area

- We have different optimizers that utilize the gradient in different ways in order to find the minimum faster
    - We will talk more about this later

- Our surfaces are not so nice, they don't ever have just one minimum
    - We can get stuck in local minima, which stinks
    - These can have either saddle points (where the slope is zero but you aren't at a minimum) or local minima



