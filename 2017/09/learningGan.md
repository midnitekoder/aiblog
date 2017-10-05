## Learning Generative Adversarial Networks

### Prerequisites
[For introduction and use cases of GANs](https://www.analyticsvidhya.com/blog/2017/06/introductory-generative-adversarial-networks-gans/)

[For detailed explanation and code](https://wiseodd.github.io/techblog/2016/09/17/gan-tensorflow/)


Some terms which you may not be aware of:

#### [Marginal distribution](https://en.wikipedia.org/wiki/Marginal_distribution)

#### variational autoencoders

#### Mode Collapse Problem
Since the goal of the optimization is the maximum likelihood, the training assumes single modal distribution where the center of mass lies. So it tries to favour/adapt the generated distribution of the Generator to a single mode (generally the mode with maximum frequency). Thats the reason that GANs are able to produce realistic looking images but with less variation.



### Some Musings

GAN sound like an interesting method for learning because it learns features specific to the characteristics a dataset and then this learning can be transfered to any classifier by taking the second highest convolution/fully connected layer and then, selecting the last layer based on the size and type of the dataset( which is a complete discussion in itself). GAN has a discriminator and a generator. Discriminator decides whether the fed image is real or not and based on its prediction, the surrogate function is updated and its value is back propagated for weights and bias tuning. While discrimator is trained, generator is not updated and vice versa. The goal of the discrimator is to maximize the cost function that gives more confidence to the real image classified as real and fake image classified as fake. While goal for the generator is to minimize the likelihood of fake image predicted as fake. 

Now this whole process of training the model can be thought in an n-dimentional space where ```n``` is the number of parameters to be trained in the discriminator. In this n-dimensional space, we evaluate the surrogate function and we are looking for the local maximas or saddle points. Let surrogate function be f(x,gx)=h(x)+j(gx). Howerever the goal of the generator is to minimize j(gx). So, one part of the f is constantly minimized while the other part is constantly maximized and the place to evaluate f in the n-dimensional space is varing based on bother h and j. This explains why training GANs is a difficult task.

Some problems that GAN suffers is the lack of spatial orientations and relevance to the real world as there are examples where in a generated image a dog has 3-4 eyes which do not happen in the real world, also, lack of three-dimensional orientation. GAN suffers from these defects because the function it tries to optimise is based on the goal to maximise likelihood of detecting a real image(class 1) with high confidence and a fake image with 
![image](https://wiseodd.github.io/img/2016-09-17-gan-tensorflow/algorithm.png)

### Some experimental findings 

In the DCGAN paper, there is a small section where the authors use discrimator of the GAN and remove its final layer and use the remaining trained model to extract features of images of CIFAR-10 to further use it for classification and they got good results though not as good at state-of-the-art supervised learning based methods. I tried to do some experiments to see how good it can be and I think that they cannot beat state-of-the-art because GAN is basically learning to map one distribution(p_z) to another distribution(p_data). It doesn't mean that it is generalizing the other distribution (one reason could be mode collapse problem) and other important point to note is that GAN doesn't know anything about data of any other distribution. So if new distribution (p_r) is different from the p_data, the discriminator of the GAN cannot give good results. So this mode of classification lacks transfer learning abilities if the dataset distributions are different.


### Papers read

#### [Unsupervised representation learning with deep convolutional generative adversarial networks](https://arxiv.org/pdf/1511.06434.pdf)

