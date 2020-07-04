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
## About submission
