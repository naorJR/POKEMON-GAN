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
In this model we added 2 networks : encoder and another discriminator.
The idea behind this model is to create another network that transform an image into a latent vector,and to creat "2 way  road" : a generator that transforms a latent vector to an image and an encoder that does the opposite way.
Now we will have to work with 2 discriminators - one for the images and one for the latent.

## THE Architecture :

![image](https://user-images.githubusercontent.com/93729949/173030977-b89d9437-8fdb-4cd2-9137-c2f75231e52b.png)

G - Generator , E - Encoder , D_z - Latent Descrrimnator , D_x - Image Discriminator
The general idea about the training is the same as before but now we  have two source of fake images - G(Z) AND G(E(X)).
E and G try to minimize this loss while Dx and Dz try to maximize it. G tries to trick Dx into believing the generated samples x_hat and the autoencoded samples x_tilde are real, while Dx tries to distinguish those from the real samples x. E tries to trick Dz into believing the generated samples z_hat and the autoencoded samples z_tilde are real, while Dz tries to distinguish those from the real samples z. G and E have to work together so that the autoencoded samples G(E(x))=x_tilde are similar to the original x, and that the autoencoded samples E(G(z))=z_tilde are similar to the original z.




The result :


![image](https://user-images.githubusercontent.com/93729949/173015031-af71119e-97c7-42bc-8305-02c26cf16a6f.png)

### References:
https://towardsdatascience.com/autoencoding-generative-adversarial-networks-16082512b583
https://jovian.ai/aakashns/06b-anime-dcgan
https://machinelearningmastery.com/how-to-implement-the-inception-score-from-scratch-for-evaluating-generated-images/

