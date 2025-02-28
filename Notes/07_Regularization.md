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

## Ensembling

- We can train multiple models, then combine their results to get a final prediction
- We can sample the data with replacement
- We can do this either by giving each model an equal vote in the final answer or by weighting their vote based on their accuracy with their samples of the data

## Dropout

- This is like ensembling
- We can drop some of the neurons for each training instance or batch
- This forces the network to learn how to do its task without receiving the whole picture
- This also keeps the network from relying too heavily on a specific set of neurons

## Adding noise

- This is especially good when we don't have a lot of data
- We "make up" new data based on the points we already have
- By smearing the data out in this way, we allow our model to be more smooth and not aim to get through all the original points

## Bayesian approaches

- We split up the probability distribution of the output given the inputs and the training data into the probability of output given the inputs and the weights and the probability of the weights given the training instances
- The weights are not all equally likely (each setting of the weights is a new model, and each model does only so well with the training data)
- So, some settings are more probable and should affect the actual model more than other settings
- Thus, each weight is not really a discrete number, but rather a probability over some values
- How do we find the probability of the weights given the training instances?
    - It is just the probability of a single y, given its x and the current weights, multiplied by the prior of the weights
    - So how do we find the prior of the weights given nothing? How do we find what "nature intended it to be" for each weight?
        - We don't know... we can only really guess...

## Transfer Learning

- We have a really good trained model that does something
- Then, maybe we don't have a ton of data for something else, so we take our really good model that does something similar to what our new task is
    - We use the input from the really good model and fine-tune it to our new task

## Multi-task learning

- We take a model and make it give two different outputs
- The two tasks share most of the weights, but the model has a head for each output

## Self-supervised learning

- We train the model with data that is missing parts and have it fill those pieces back in

