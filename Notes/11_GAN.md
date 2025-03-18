# GANs

- There are two parts to the network:
    - The generator takes random noise and creates some sample that we are trying to mimic
    - The discriminator takes real data and the generated data and tries to learn how to differentiate between them

- What is the loss function for the GAN?
    - The discriminator just does a nice standard cross entropy loss
        - We use $-log(1 - sigmoid(f[x_j^*, \phi]))$ for the bit about the fake data

        - We use use $-log(sigmoid(f[x_i, \phi]))$ for the bit about the real data
    - The generator is just trying to optimize its parameters, $\theta$, in order to maximize the loss of the discriminator
    - So, we have two loss functions
        - One that is focused only on $\phi$ and tries to minimize the loss (the Discriminator)
        - One that is focused only on $\theta$ and tries to maximize the other's loss (the Generator, it just removes a negative sign to go the other way)

## Some problems and solutions

- To start out, the Generator is really bad because it is starting with random noise, the data is distant and the gradient is almost non-existent 
    - We use Wasserstein distance, which gives us finite distances even with things that are very far apart
        - This is dependent on how much "dirt" you have to move, and how far you have to move it
    - This gives us a new loss function that makes the gradients better
- It's hard to make good resolution data right at the get go
    - Let's start by making smaller versions of the data, lower resolution, and training the model with that
    - Then, when that is good enough, we add more layers to each part of the model and go again until we grow to the size we want
- We can use mini-batch stats of the real images and feed those to the discriminator as well
    - We then have to make the stats (the variation) of the Generator match those of the real images in order to fit better
- We can do truncation
    - This is when we choose random values that are only within a certain threshold from the latent distribution for our Generator
    - With a higher threshold, we get more variation, but things look a little funkier
    - With a lower threshold things start to look better, but also more of the same (low enough and it's all the same)
- We can use interpolation to check the model
    - A linear transformation in the latent space should mirror a linear transformation in the real space
    - This is less true for things that are super far apart

## Conditional GANs

- We pass a random vector of the latent space, as usual
- We also pass some conditional vector (Something that is still usual but tells the GAN about the class we want or something about what we want the picture to look like)
- The GAN generates both, the Discriminator sees if the GAN's output pair of the image and the conditional are real
- We can do something similar but where the Discriminator only receives the image from the Generator (not the conditional) and has to put out the probability the data is real AND give out the conditional with which the Generator made its image
    - This allows us to learn about things in the image and therefore use it to generate new images with specific details we want

## Image translation

- We can input not random noise but some altered version of real data
- We get the Generator to make the real image from the altered one (like from B/W to colored)
- We get content loss from seeing if the generator makes something that looks like the real image
- We also get the Discriminator see if the pairing of the input data and the output are real
