# Style Transfer

- This is really all about our loss function
- We are not going to be turning the weights, but rather the input data
- Something funky about this is that there isn't really a "right" answer for what you are doing, so you have to know how to construct the loss function

## How do we do it

- We are going to separate the style and content
    - Style is for the lower layers
    - Content is for the higher layers
- Synthesize a new image such that
    - Lower level stats match style activations
    - Higher level stats match content activations

## Details

- We are going to use VGG (A vision network)
- We are not going to use the last part of it (the fully connected layers)
- We are not going to move their parameters at all. We will only pass forward our image and pass back the gradient all the way to our image to update the image
- We have three networks
    - One to take the style image -> we read out the activations (the ReLU outputs) at many points
    - One to take the content image -> we read out the activations at one point
    - One to take a new image (actually just the content image again) -> we read out both content and style activations
        - We are going to change this image ("adjust its weights") in order to make its activations look like the other two networks
        - We are going to make a loss function that tells us how well this is doing and that is what we train

## On content and style

- We only look at the content activations once because this doesn't change a ton throughout the network
- We look at the style activations at multiple times because its representation changes a lot throughout the network

## The Loss function

- Our total loss is as follows:
    - The total loss is dependent on three things: the content image, the style image, and the generated image and is a weighted sum of two losses:
        - The content loss (Weighted by a constant) is dependent on the content image and generated image
            - This is simply 1/2 the sum squared loss of the content image activations and generated image activations at a specific layer
                - The activations are 2D matrices that have height equal to the number of filters and width equal to the H x W of the image
                - Since we are taking the difference at each point, we preserve the local statistics
        - The style loss (weighted by a constant) is dependent on the style image and generated image
            - This is a bit more complicated, and it doesn't any longer preserve local statistics (which makes sense because we don't need neighboring data to be similar, we care about details across the whole image)
            - This has to do with the Gram matrix:
                - The size is the number of feature maps squared
                - This is a pairwise inner product of all the feature maps in a specific layer
                - Each entry in the matrix is a scalar that results from this dot product to tell us how similar the different feature maps are
            - The actual loss is a weighted sum of the normalized mean-squared error between the Gram matrices of the style image and generated image
