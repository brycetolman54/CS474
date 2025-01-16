# Shallow Networks

- We define a loss function to tell how well we are approximating the data and to know how to improve our predictions
- Activation functions are the things that allow us to have non-linearity in our models
- A simple network:
    - $y = \phi_0 + \phi_1h_1 + \phi_2h_2 + \phi_3h_3$
    - $h_1 = a[\theta_01 + \theta_11x]$
    - a is the activation function
    - $\phi$ and $\theta$ are the knobs (the weights that we can change between the input and hidden layers and the hidden layers and the output)

- Universal Approximation Theorem:
    - We can fit any 2D function with enough hidden units, somebody proved it...

- With more neurons, we can include more inputs and more outputs
    - An example of 2 outputs: we need to output an image and a text description of that image
        - We give both heads (output nodes) the same last layer info and they generate their own things describing the same thing

