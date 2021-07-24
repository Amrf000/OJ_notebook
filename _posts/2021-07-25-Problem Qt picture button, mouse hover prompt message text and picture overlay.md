---
layout: post
title: Problem Qt picture button, mouse hover prompt message text and picture overlay
category: qt5
tags: [qt5]
---
# 

1\. Picture button: Open the .ui file in Qt Creator, select pushbutton and right-click\> change style sheet\> add resource\> border-image\> select the picture in the resource\> OK. When finished, select the picture button in the object tree on the right to see the style sheet.

![](/public/assets/2021-07-25/1dbdcd6fecce64ddcfbeaa330e3d2223.png)![](/public/assets/2021-07-25/13f3425821d13c51b9c9462a7994a27c.png)

2\. Select tooltip in the attribute table on the right, and enter the prompt information when the mouse hovers over the button.

![](/public/assets/2021-07-25/ba4225f7054a863290664ca1997a58eb.png)

Question: When the email is hovering, the prompt message is superimposed on the text and the picture used. autoFillBackground does not work when it works.