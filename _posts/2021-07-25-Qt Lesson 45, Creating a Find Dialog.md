---
layout: post
title: Qt Lesson 45, Creating a Find Dialog
category: qt5
tags: [qt5]
---
# 

## 

##### 

### 

1\. Find dialog

* Find dialog is a common part in the application  
Goal: develop a search dialog that can be reused between different projects
* Requirements analysis of the search dialog:  
--- reusable software parts  
--- Find the specified string in the text box  
--- Ability to specify the search direction  
--- supports case-sensitive search
* Additional requirements:  
--- hide after clicking the close button  
![ ](./assets/2021-07-25/ad6b6061219779300a8d542feedbd2fc.png)  
The architecture and design of the search dialog:  
![ ](./assets/2021-07-25/5ab6b82f49e7d0cf662c8314eec0aa6a.png)
* Interface layout of the search dialog  
![ ](./assets/2021-07-25/0dd4cd6b44b4a620dd515310fe614c68.png)

summary:

* The search dialog can be developed as a reusable software component
* Find dialog inherits from QDialog class
* The interface of the search dialog is nested with each other through the layout manager
* The design and implementation of the search dialog is a classic example in GUI learning