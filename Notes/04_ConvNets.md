# Convolutional Neural Networks

- This is good for dealing with data that has spatial relationships
- We could deal with this data as we do other data, making it one big line of input, but that requires a TON of parameters and gets unwieldy for even simple data
- The way a convolutional net works is to look at local patches of pixels, and look at those patches across the whole image in the same way
    - The weights for one filter are shared across the whole image, so it doesn't matter where the patches are, we can recognize them
- Variance types:
    - <b>Invariance</b>: we can transform the image and still recognize the patches
        - $f[t[x]] = f[x]$
    - <b>Equivariance</b>: if we move our data, the network should put out a different result, but only because it is moved the same way the data was

## Convolution in 1D

- Our input is <b>x</b>: $x = [x_1, x_2, ..., x_I]$
- The output is a weighted sum of neighbors:
    - $z_i = \omega_1 x_{i-1} + \omega_2 x_i + \omega_3 x_{i+1}$
- The convolutional filter (size of 3 here)
    - $\omega = [\omega_1, \omega_2, \omega_3]^T$
- How do we compute the ends?
    - We can do 0 padding
    - We can just leave out the end point (not center the kernel around it)
        - This is what we call "valid" padding
- Some terms:
    - <i>Stride</i>: how many nodes we slide when we move the kernel
        - You can tell about this based on the difference in arrows between the nodes
    - <i>Kernel Size</i>: the number of nodes our window looks at
        - We can tell about this based on the number of arrows coming out of the nodes (the max)
    - <i>Dilation</i>: the space between the nodes we look at in our window
        - We can tell about this based on the difference in arrows as well
    - <i>Padding</i>: whether we include something around the edges
        - We can tell about this based on the difference in the number of nodes between the layers
- Channels
    - There are channels that each can pick up different features for us
        - Each layer only looks for one feature, so we would lose information about the image otherwise
        - We have one set of weights for each different feature map (channel)
        - We can go in reverse and combine several feature maps into a single output layer
- How much does it all cost?
    - If we have $C_i$ input channels and a kernel size of $K$, we need $C_i \times K$ weights
    - If we have $C_i$ input channels, a kernel size of $K$ and $C_o$ output channels, we need $C_i \times K \times C_o$ weights
    - That is a lot less that we needed before!

## Convolution in 2D

- This works exactly the same, except now we have another dimension
- This means more weights, but still not nearly as many as for the MLP
- We usually use a $K \times K$ kernel (a square), but we don't have to

## Other things

- We can downsample
    - This is to reduce the amount of data we are looking at in order to get a better overall picture
    - How to do it:
        - Just skip things (do a bigger stride)
        - We can max pool (grab the max of the window of pixels) -> this has some invariance to translation
        - We can do mean pooling (grab the mean of the window of pixels)
        - We do this for each channel (we don't combine the channels in doing this)
- We can upsample
    - This takes a small amount of data and increases it for us
    - This can be done in smarter or dumber ways
    - How can we do this:
        - We can duplicate, giving the same pixels from one into a window
        - We can put in the values to a new window and make them the max (make the surrounding ones 0 or something small and random)
            - We can keep track of where we grabbed the max from or we can put them in random places in the window
        - We can do interpolation (spread out the pixels and fill in the new areas with the average between the pixels)
        - We can do transposed convolution
            - Take the weight matrix and transpose it
            - If the matrix went from 8 to 4, now we go from 4 to 8 nodes
            - This is great because we can make the weight matrix learn based on the loss of how well it blows up the picture

## 1x1 Convolutions

- We don't look at neighbors, just at one pixel. Why?
- We want to mix the channels in one pixel to get a new picture of one channel that has combined the data from all those channels into one
