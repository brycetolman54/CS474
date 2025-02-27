# Regularization

- This is a way to manage the bias-variance trade-off
- There are many different ways to do this:

## Explicit Regularization

- There are hack-ish ways to do regularization, but this is one that has theoretical underpinnings
- This type of regularization just adds another term to our sum to account for what we want to do (this extra term is weighted for importance)
- For example, we can say that we don't want big weights, so we add a function to our loss that is higher for bigger weights, so we penalize big weights
- This will make us have a worse error on our training data, but makes a model that generalizes better
    - This is called L2 regularization, the sum of the square of the weights
- In the Baye's way of thinking, the regularization is the prior, what we already know about the weights before seeing them (what we already want to be true about the weights before doing anything with them)

## Implicit Regularization

- This is not actually adding a term to your loss, but it works...
- Gradient descent is actually a form of regularization, but it is not explicitly
- SGD is a different form of this: the loss hill changes every mini-batch
    - The loss in this case changes every time, and the composite of these is the regularization term
- We like large learning rates and smaller batch sizes (generally)

## Early Stopping

- It is a hack
- We look at the validation data in order to stop when it starts getting worse (after it is getting better)
- We keep the model from having time to overfit the data
