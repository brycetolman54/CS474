# Diffusion

- This is state-of-the-art for images, it has surpassed GANs
- The idea is that we have an image, gradually add noise (this is the diffusion part) and then remove it to get the image back
- Then, when we have the model, we input random noise and it pulls out an image

- What we really need is a model that can predict what is noise and what is not in our image
- For this model, we need two inputs, a noisy image and the "amount" of noise that has been put in (the amount is a timestep, how many times noise has been added)
    - The model takes those in and outputs an image of the noise
    - We take  that noise and subtract it from the image to get a denoised image (but in increments)

- We can include attention in there as well.
    - We can send in some text (in a vector embedding obviously) to influence the model and make sure that we are getting out what we want
        - We have to add this text in for the diffusion (forward) part to be able to use it in the denoising part
