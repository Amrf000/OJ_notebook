---
layout: post
title: Qt to achieve simple picture reflection effect
category: qt5
tags: [qt5]
---
Support original text:[https://www.fearlazy.com/post/274.html](https://www.fearlazy.com/post/274.html)
Idea:
To get the reflection effect of the picture, first get the symmetry picture of the picture, and then translate the picture to be translated.
The symmetry image to get pictures in Qt only needs to call the qimage's mirrored function, which returns a mirror qimage object for qimage. Depending on the parameters
Mirror images in both horizontal and vertical two directions.
Semi-translation can be implemented by setting the opacity of QPainter (call QPainter's setopacity).
test:
![](/md_blog/public/assets/2021-07-25/c1106e719be9f155fcb44ec5a7904020.png)
The code is not much easily understood. First, Painter draws the original image in the position of (50, 50), then call the mirrored () to get the mirror image, then set the opacity of the Painter to 0.3, and finally 2 pixels below the original picture. Location drawing mirror image.
Test Results:
![](/md_blog/public/assets/2021-07-25/619efffe49906f605c74095fe4bd11d1.png)
Special Note:
If you subsequently discovered errors in your article, you will only be updated in my personal blog. My blog mainly records the knowledge of the programming, the pit and some inexplicable ideas, I don't pick language, but I will be based on C ++, welcome to step on my blog: Fearlazy.
