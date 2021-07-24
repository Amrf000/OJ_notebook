---
layout: post
title: Qt Lesson 23, File Operations in Qt
category: qt5
tags: [qt5]
---
# 

## 

* The text editor involves saving text and reading text, so today we will learn about file operations in Qt.

1\. IO operations in Qt

* How to handle IO operations in Qt  
--- Qt passedUnified interfacesimulatetextversusexternal deviceThe way of operation  
--- The file in Qt is regarded as a special external device  
--- The file operation in Qt is the same as the operation of the external device
* Key function interface in IO operation  
![ ](/public/assets/2021-07-25/1ec84b96ac03acfee02872638f2ed469.png)  
The nature of IO operations: Data reading and writing in continuous storage space
* Qt`IO` Type of equipment  
--- sequential access device  
　　 onlySequential reading and writing device from the beginning, Can not specify the data read and write location  
--- random access device  
　　Can locate to any position to read and write data
* Inheritance hierarchy of IO devices in Qt  
![ ](/public/assets/2021-07-25/8fa6b6af26fd454712c6231afbd2b8a8.png)  
2\. File operations in Qt
* `QFile` Is a class for file operations in Qt
* `QFile` The object corresponds to a file on the computer  
![ ](/public/assets/2021-07-25/2f0f1e302048b2d9076482f946866904.png)
* `QFileInfo` Class is used to read file attribute information  
![](/public/assets/2021-07-25/5b0c265d8d25a8422f086ea398b67304.png)