---
layout: post
title: QT_Widgets button style sheet (1)
category: qt5
tags: [qt5]
---
# 

## QT\_Widgets button style sheet (1)

Demo:

* New project -\> click ui interface -\> drag in a plain pushbutton

![ pushbutton](/public/assets/2021-07-25/e3cf6349630c10130ee97560148eb9ff.png)

* Right click on pushbutton-\> select change style sheet -\> enter mystery code

![ ](/public/assets/2021-07-25/7dcf07795148e73feb7332547acffb34.png)  
The mysterious code is as follows:
    
    QPushButton{color: rgb(255, 255, 255);background:rgb(0, 170, 255);border:1px solid grey; border-radius: 8px;} QPushButton:hover{border-color:rgb(139,170,105);background:rgb(0, 161, 241);} QPushButton:pressed{border-color:gray;background:rgb(0, 153, 230);} 
    

* 1

* 2

* 3

* Explanation of the mysterious code:

QPushButton： Normal style of the button  
QPushButton:hover： The style of the mouse when hovering over the button  
QPushButton:pressed： Style when the button is pressed  
color： font color  
background： Background color (the color of the pushbutton button)  
border：1px： The width of the border, the value can be changed;solid grey： Border color, want to modify the border color, change the gray, such as rgb (255, 255, 255) or rgb (0,0,0),note: "solid" cannot be deleted

* Dangdang! The button style is as follows  
![ ](/public/assets/2021-07-25/b34e87949c879f059abf5c395d63ee8a.png)

(Leadership Education)