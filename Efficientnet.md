## What happenned before efficientnet ?
- Convolutional neural networks (CNNs) are commonly developed at a fixed resource cost, and then scaled up in order to achieve better accuracy when more resources are made available. 
- For example, ResNet can be scaled up from ResNet-18 to ResNet-200 by increasing the number of layers
- The conventional practice for model scaling is to arbitrarily increase the CNN depth or width, or to use larger input image resolution for training and evaluation. 
- While these methods do improve accuracy, they usually require tedious manual tuning, and still often yield suboptimal performance.
- A novel model scaling method that uses a simple yet highly effective compound coefficient to scale up CNNs in a more structured manner. 
- Unlike conventional approaches that arbitrarily scale network dimensions, such as width, depth and resolution, our method uniformly scales each dimension with a fixed set of scaling coefficients. 
- Powered by this novel scaling method and recent progress on AutoML, we have developed a family of models, called EfficientNets, which superpass state-of-the-art accuracy with up to 10x better efficiency.

## Family of efficientnet
![family of efficientnet](https://1.bp.blogspot.com/-Cdtb97FtgdA/XO3BHsB7oEI/AAAAAAAAEKE/bmtkonwgs8cmWyI5esVo8wJPnhPLQ5bGQCLcBGAs/s640/image4.png)

## Comparison with other CNN models
![comparison with other models](https://1.bp.blogspot.com/-oNSfIOzO8ko/XO3BtHnUx0I/AAAAAAAAEKk/rJ2tHovGkzsyZnCbwVad-Q3ZBnwQmCFsgCEwYBhgL/s640/image3.png)
