---
layout: post
title: Qt Lesson 41, Realization of Editing Interactive Function
category: qt5
tags: [qt5]
---
# 

## 

##### 

### 

1\. The text editor implements copy, cut, paste, undo, and redo operations

* General editing interactive functions in the editor:  
![ ](/md_blog/public/assets/2021-07-25/67d3879a4766641ee86efa61030254c1.png)
* QPlainTextEdit provides a rich interactive function interface:  
![ ](/md_blog/public/assets/2021-07-25/7c6475639bf69245624d64ea191f0da2.png)
* Connection of signal and slot:  
![ ](/md_blog/public/assets/2021-07-25/c0ce5904a6dbbafcf12cf925101c9026.png)  
We only need to bind signals and slots to events created in the menu bar or toolbar:

1.2 Interface state maintenance

* The state of the interface in the text editor requires manual maintenance by us: not always copy, paste, undo, redo  
![ ](/md_blog/public/assets/2021-07-25/aec619d7c51794d91119858032bc6de6.png)
* QPlainTextEdit can send signals related to interface status:  
![ ](/md_blog/public/assets/2021-07-25/0243da274f3f31a95ec4c50b3ca0a127.png)
* Implementation steps  
1\. Connect the interface status signal to the custom slot function  
2\. Find the corresponding QAction object through text information  
3\. Set the interface state of the QAction object according to the signal flag

summary:

* QPlainTextEdit encapsulates commonly used text editing functions
* You can connect the signal directly to the public slot function of QPlainTextEdit
* The interface state is the focus and difficulty of GUI development
* The status signals of components in Qt can simplify the maintenance of interface status
* The components of the main window can be retrieved by traversing