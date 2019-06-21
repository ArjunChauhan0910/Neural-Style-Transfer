# Neural-Style-Transfer

Tensorflow Implementation of Neural Artistic Style Transfer using VGG-19.

## Dependancies
* Tensorflow (1.13.1)
* Numpy (1.16.4)
* Matplotlib (3.1.0)
* Scipy (1.2.0)
* PIL (5.1.0)
* The weights for the model [VGG19](https://arxiv.org/pdf/1409.1556.pdf) can be downloaded from [here](http://www.vlfeat.org/matconvnet/models/imagenet-vgg-verydeep-19.mat)

## Steps for Implementation

1. There are 2 images which are required for the implementation of this application. One image is the _Content Image_ and the other is the _Style Image_. The _Content Image_ is styled ( implemented with similar style/patterns ) with respect to the _Style Image_. A standard _Noisy Image_ is generated whose pixel values are subsequently changed as the iterations proceed.
2. A feature vector representation of the images (Content, Style and Generated) is extracted from an intermediate layer of the network. If the intermediate layer is one of the shallower layers then more importance is given to the pixel values (which effectively means the content of the image). If the intermediate layer is a deeper layer then more focus is put on the style of the image and not their relative position. Depending on the layer chosen, more importance can be given to content or style.
. Hereby a loss function is defined which is a combination of one loss function for the _Content image_ and _Generated image_ and one loss function of _Style Image_ and _Generated Image_. The total loss is dependent on two hyperparameters: alpha and beta. The total loss is thus defined as _Alpha x L(ContentImage, GeneratedImage) + Beta x L(StyleImage, GeneratedImage)_ where _L(A,B)_ is a function used to define the loss. Here L2 norm is used as the loss function.
4. For the _Content and Generated Image_ pair, the loss( _L(ContentImage, GeneratedImage_ ) is directly found by unrolling the vectors obtained from the intermediate layers and finding the L2 norm. For the _Style and Generated Image_ pair, a correlation vector across the various channels is taken. This is done using [gram matrix](https://en.wikipedia.org/wiki/Gramian_matrix) and then the loss ( _L(StyleImage, GeneratedImage)_ ) is calculated.
In this particular implementation, the style is taken across various layers unlike the case of Content Image. This is done to get a better sense of the style into the _Generated Image_
5. The total loss function is then calculated and optimized using Adam optmizer to get the final styled image.

## Takeaways

1. VGG19 is being used as a feature extractor in this application. These features are used for extracting the style and content of the image. The way it works on style extraction is particularly interesting. The result is obtained from a set of features (like ex corners/edge) and colors/patterns and how they are inter-related. Since the similarity is taken across various channels and layers, a more coherent representation of the style can be captured.
2. The loss function which is optimized is basically the distance between the different representations i.e. Content image representation, Style Image representation and Generated Image representation.
3. VGG based architectures are better suited to this application as it does not downsample the image much unlike other architectures like LeNet. Also, the VGG architecture has features that are more condense and not spread across various layers thus making it optimal for style extraction.
 



## References
* [A Neural Algorithm of Artistic Style](https://arxiv.org/pdf/1508.06576.pdf)
* [Artistic Style Transfer with Convolutional Neural Network](https://medium.com/data-science-group-iitr/artistic-style-transfer-with-convolutional-neural-network-7ce2476039fd)


## Results
### Content Image
![Content Image](/japanese_garden.jpg)
### Styled Image
![Style Image](/picasso_selfportrait.jpg)
### Final Result
![Style Transfer Image](/StyledImage.jpg)
