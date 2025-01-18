# Deep Networks

- When we have more than one layer, the output from one layer just becomes the input for the next layer
    - All the functions are the same, we just have a different input than $x$
- Pretty much, for each section of the first network, we get a copy of the second network's function on that section
    - This is why we the number of sections grows exponentially with <i>K</i>, the number of hidden layers
- We were able to, before, have a network with multiple heads (outputs), but the same body (the same earlier nodes)
    - With a multi-layer network, that same thing is happening, but the "heads" are just the nodes in the next network
    - Each one gets all of the information from the previous node, and then does its stuff
- Here are some hyperparameters:
    - $K$ - the number of layers (depth)
    - $D_K$ - number of nodes in the layer (width)
- 
