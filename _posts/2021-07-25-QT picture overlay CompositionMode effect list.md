---
layout: post
title: QT picture overlay CompositionMode effect list
category: qt5
tags: [qt5]
---
1. QPixmap tmpPix(pix.size());
    

2. tmpPix.fill(Qt::transparent);
    

3. QPainter p1(&tmpPix);
    

4. p1.setCompositionMode(QPainter::CompositionMode_Source);
    

5. p1.drawPixmap(0, 0, pix);
    

6. If (canBuild) / / can be built with a semi-transparent representation
    

7. {
    

8. 	 //200 for transparency, 0 for full transparency, and 255 for opacity
    

9.  p1.setCompositionMode(QPainter::CompositionMode_DestinationIn);
    

10. 	p1.fillRect(tmpPix.rect(), QColor(0, 0, 0, 200));
    

11. }
    

12.  Else / / can not be built with red translucent
    

13. {
    

14. 	p1.setCompositionMode(QPainter::CompositionMode_ColorBurn);
    

15. 	p1.fillRect(tmpPix.rect(), QColor(255, 100, 100, 200));
    

16. }
    

17. p1.end();
    

18. pix = tmpPix;
    

19. painter->drawPixmap(fzX1 - NODE_WIDTH + thisBuilding.x_draw, fzY1 + NODE_HEIGHT + thisBuilding.y_draw, pix);
    
    

First on the same paragraph of the online code, it will be seen, not so much time to write a post

CompositionMode\_DestinationIn

![](./assets/2021-07-25/d0d1583b1db1c52087c63b09b693b097.png)

CompositionMode\_ColorBurn

![](./assets/2021-07-25/da7ad9541fe2daf5c858f55ea5cac9bb.png)

CompositionMode\_ColorDodge

![](./assets/2021-07-25/3d161b2ed2b4d3f6f349241ae6098b93.png)

CompositionMode\_Darken

![](./assets/2021-07-25/3a3466d48bdb835797a5f444240f0396.png)

CompositionMode\_Destination

![](./assets/2021-07-25/5cad023c9b6214b16065825dbe815b9a.png)

CompositionMode\_DestinationAtop

![](./assets/2021-07-25/212addc3bc7e214b31bfaa8261a929aa.png)

CompositionMode\_DestinationOut

![](./assets/2021-07-25/0eaa67264f600a9a2d5b70925507a001.png)

CompositionMode\_DestinationOver

![](./assets/2021-07-25/9537ca88f464cb9fdea008ee4e8ad45b.png)

CompositionMode\_Difference

![](./assets/2021-07-25/3608746bb8fb888b603f032ab09c84d9.png)

CompositionMode\_Exclusion

![](./assets/2021-07-25/dbf17f2d03fc730cf5e88b85f98b3d56.png)

CompositionMode\_HardLight

![](./assets/2021-07-25/842842dad4e997410673a5661b82d8a0.png)

CompositionMode\_Lighten

![](./assets/2021-07-25/7784453aa2db89a8a052e66039bf408a.png)

CompositionMode\_Multiply

![](./assets/2021-07-25/60844f8ebafbd668f7e5e9135c5ae151.png)

CompositionMode\_Overlay

![](./assets/2021-07-25/71048778b669f6b8b91ef9b3dd25382e.png)

CompositionMode\_Plus

![](./assets/2021-07-25/e08b5b7c0a1293810174285c15b61d4b.png)

CompositionMode\_Screen

![](./assets/2021-07-25/1099a6047848483c2d9e951a524f86d2.png)

CompositionMode\_SoftLight

![](./assets/2021-07-25/ef9b6217e0fd270456cb95c203f95f86.png)

CompositionMode\_Source

![](./assets/2021-07-25/1599e2b5ffb363a543c127f09e678963.png)

CompositionMode\_SourceAtop take the intersection

![](./assets/2021-07-25/bc5819f6e9bef3d4088aca9a72977df1.png)

CompositionMode\_SourceIn 

![](./assets/2021-07-25/21231d816afce13a184e7d060f918e80.png)

CompositionMode\_SourceOut This is directly hollowed out

![](./assets/2021-07-25/88a35a772d6a4b0e4ed2e50efe71da0f.png)

CompositionMode\_SourceOver

![](./assets/2021-07-25/7cae5a9307b43ef6123aff5bb25603bf.png)

CompositionMode\_Xor 

![](./assets/2021-07-25/7698208aa2c81fe5d502d7aa907dc844.png)

[](http://qtxlsx.debao.me/)