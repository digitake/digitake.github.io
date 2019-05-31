---
layout: post
title:  "keras.image_utils.preprocess_input"
date:   2019-05-31 14:30:00 +0700
categories: Python3, Tensorflow, Keras, ML
comments: yes
---

`preprocessing_input` function is to adjust the input tensor to be able to consume by the backend.
According to keras's document:

If `mode` parameter is:
- caffe: will convert the images from RGB to BGR,
                then will zero-center each color channel with
                respect to the ImageNet dataset,
                without scaling.
- tf: will scale pixels between -1 and 1,
    sample-wise.
- torch: will scale pixels between 0 and 1 and then
    will normalize each channel with respect to the
    ImageNet dataset.
```
