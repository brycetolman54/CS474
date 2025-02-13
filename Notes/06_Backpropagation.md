# Backpropagation

- This is how we get the loss for each of the layers in the network as we go back through it
- We could get the gradient like this:
    - The whole network is one big function (The loss too) based on all the $\beta$ and $\Omega$
    - We could just take a derivative with respect to all of the parameters, but this is super lengthy and stupid
    - We don't want to do that, especially when we have a ton of parameters
- So how do we actually do it?
    - We save the forward pass
        - We do the weighted sum of the inputs to get a value (f), that we keep (this is before the activation function)
        - We do this from the inputs to the outputs
        - This gives a dependency graph (which is just a line in a simple function)
    - We do the backward pass
        - We have to go in reverse order, from output layers to input layers
        - We get the loss, and we find the partial derivative with respect to the last function of the chain
        - We then move back and find the partial derivative of the next one back (the dependency is in the other direction)
            - This allows us to find the loss of earlier things in the network even though they have to pass through so much to get to the output
        - We find the derivatives of things in the final layers and then use those to get the derivatives of earlier layers
            - We can't just derive the loss with respect to the function output, but rather we have to finally find the derivative with respect to the parameters that we are tuning
    - It is a good thing that the activation functions are derivitable, as we get their derivative
    - We have to keep the forward pass in order to get the backward pass working
- When we get to a big network, this dependency graph gets terribly big, but we still have our simple algorithm for getting the derivatives


# Initialization

- We have to set the weights and biases to something to start, how do we do it?
- WE can't set the weights to be 0, because backprop relies on the weight values to update, so if all are 0, nothing changes
- We can set the biases to 0, as backprop does not depend on it, so they can change
- We want the mean of our weights to be around 0 so we have some that are negative to cancel those that are positive
- What about the variance of them then?
    - We can't have it be too small, as it will vanish
    - We can't have it be too big, as it will explode
    - So... let's enforce the weights to have the same variance at each layer
        - We can do some algebra things and see that we need $\sigma_{\Omega}^{2} = \frac{2}{D_h}$
        - He initialization is what this is called (this is specifically for a ReLU)
