# POKEMON-GAN
<p align="center">
<img align="mid" src="https://raw.githubusercontent.com/naorJR/POKEMON-GAN/main/Images/International_Pokémon_logo.svg.webp"></a>
</p>
Generating Pokemon with a Generative Adversarial Network

## Overview:
In this project i coded 3 diffrent models - AEGAN,DCGAN14000,AEGAN819,in order to generate fake pokemons.

## Guide :
Every model has its own folder and in each folder we can find a link to the data set, result images, ipynb of the model and 
the weigths of the network.

## DCGAN819 :

In this model i created 2 network : generator and discriminator.The dataset used to train this model has only 819 images.

Generator Model

The input to the generator is typically a vector or a matrix of random numbers (referred to as a latent tensor) which is used as a seed for generating an image. The generator will convert a latent tensor of shape (latent_size , 1, 1) into an image tensor of shape 3 x image_size x image_size. To achive this, we'll use the ConvTranspose2d layer from PyTorch, which is performs to as a transposed convolution (also referred to as a deconvolution).

Discriminator Model

The discriminator takes an image as input, and tries to classify it as "real" or "generated". In this sense, it's like any other neural network. We'll use a convolutional neural networks (CNN) which outputs a single number output for every image. We'll use stride of 2 to progressively reduce the size of the output feature map,we could use maxpolling instead of stride .

## Train 
![image](https://user-images.githubusercontent.com/93729949/173016809-6dd18aff-656a-403b-8eec-27ec6cfcad5e.png)

How do we train the generator :

- We generate a batch of images using the generator, pass the into the discriminator.

- We calculate the loss by setting the target labels to 1 i.e. real. We do this because the generator's objective is to "fool" the discriminator.

- We use the loss to perform gradient descent i.e. change the weights of the generator, so it gets better at generating real-like images to "fool" the discriminator.

How do we train the discriminator :

- We expect the discriminator to output 1 if the image was picked from the real dataset, and 0 if it was generated using the generator network.

- We first pass a batch of real images, and compute the loss, setting the target labels to 0.85 + gaussian noise (smoothing label).

- Then we pass a batch of fake images (generated using the generator) pass them into the discriminator, and compute the loss, setting the target labels to 0.15 + gaussian noise.

- Finally we add the two losses and use the overall loss to perform gradient descent to adjust the weights of the discriminator.

The result :

![image](https://user-images.githubusercontent.com/93729949/173014816-bb673177-6c04-422e-a357-3d069d5967a6.png)

## DCGAN14000 :

The only diffrence between this model and the previous model is the dataset that used to train the 2 networks,here i use a much larger dataset with 14000 images.

![image](https://user-images.githubusercontent.com/93729949/173015100-ec6df66b-2d8a-47da-8a78-cff3df6bbc2e.png)

## AEGAN :

![image](https://user-images.githubusercontent.com/93729949/173015031-af71119e-97c7-42bc-8305-02c26cf16a6f.png)



