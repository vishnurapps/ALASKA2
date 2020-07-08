## About the competition
- This competition is about identifying if someone had added hidden information in images using stenography
- We need a deep learning solution as the current methods are un reliable and cause false alarm
- The three main methods to do stenograpy are JMiPOD, JUNIWARD and UERD
- Usually images have 3 channels (RGB), composed by pixels, which describe the image (the colors).
- There is a python module called Stegano, it hides the hidden information in the least significant bits of the image. 
- These bits have the property of being very random (white noise), so they don't fire when some change is applied to them.
- all images are 512 x 512 x 3
= all images are of size 786,432
- all images are uint8 type
![Conversion of raw image to jpeg](https://i.imgur.com/c54ht2c.png)
- Images can be hidden in YCbCr channels. This is an old approach
- Images can also be hidden in the DCT coefficients of the YCbCr channel. The payload (secret information) is randomly distributed
- A discrete cosine transform (DCT) expresses a finite sequence of data points in terms of a sum of cosine functions oscillating at different frequencies.
- transformation tenchnique for data compression
- uses cosine rather than sine (faster computation)


## Code samples
## About models
- Either YCbCr or DCT Coeff can be used as inputs to the neural net
- This problem can be solved as a binary classification problem. But solving as a [multiclas problem](https://www.kaggle.com/c/alaska2-image-steganalysis/discussion/155821) seems to be better
## Insights from leaders
- Don't resize. Any perturbation to original pixels will obliterate all hidden message (which is already a very weak signal). So don't resize, rotate or re-save images during training
- Augmentation with flips and 90-degree rotations are OK.
- Crops are useless. In a sense, training on full-sized 512x512 tends to provide higher AUC score on all model architectures I've tried so far
- Training on YCbCr colorspace is doubtful IMO. At the end of the day, YCbCr RGB conversion is a linear combination and any CNN model will learn it with ease
- Normalization is very important. Don't forget to do proper (at least ImageNet-like) normalization for your input data
- Bronze with Resnet34 is doable. It's faster to train than heavier models, but shows immediately if there is something wrong with your pipeline.
- The way you read JPEGs is irrelevant. As long as you read images the same way for training & testing you're good.
- TTA helps, but up to some point. After 0.92 it worsens the score.
- You can solve this problem as binary- and multi-class classification. Multi-class seems to be a bit better, but it's not written in stone.
- Bigger batch is better. I'm strongly suggesting to leverage fp16 training or if you know how to do model surgery - give a try to InplaceABN.

##Advantages of tfrecords

Reading each individual image in the large dataset is often a slow process. So, to make it fast we store many images as tensor Tf records and read from there.
At a time, we can feed data from many TF records to TPU for training without worrying about the order. This will make the data feeding process fast and hence improve the overall run time.

## Models to try
MobileNet, MixNet, and EfficientNet - Depthwise separable convolutions are common between these backbones.

Expanding on this idea… FBNet, MNASNet, SinglePath NAS also converge, but don't achieve as high an accuracy as the bigger Efficientnets (they tend to level off in the Efficientnet B0-B1 range). So I'd say more generally that backbones based on the MobileNet V1/V2 block sequence tend to work. More work to do on understanding why this is the case.
This observation can also form the basis for custom network design.
## About submission
## Important links
- FP16 : https://www.quora.com/What-is-the-difference-between-FP16-and-FP32-when-doing-deep-learning
- Tips Discussion : https://www.kaggle.com/c/alaska2-image-steganalysis/discussion/155392
- Model Surgery : https://www.kaggle.com/neongen/minimum-vram-footprint-gpu-baseline
- Discussion on model Surgery : https://www.kaggle.com/c/aptos2019-blindness-detection/discussion/104686
- Basics of AUC-ROC : https://www.dataschool.io/roc-curves-and-auc-explained/

## Experiments
|Version|Changes in models|Changes in Augmentation|batch size|Validation loss |validation auc score|public leader board score|
|-------|-----------------|-----------------------|---------------|----------------|-------------------------|
|v1(base forked)|Used efficientnet|horizontal flip, vertical flip|32|58.146|0.799|NA|
|v2(My first attempt)|replaced efficientnet with resnet34|Added 90 degree rotation|32|0.108|0.788|0.601|
