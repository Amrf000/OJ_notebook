---
layout: post
title: Qt Lesson 59, Custom Model Class (Medium)
category: qt5
tags: [qt5]
---
# 

## 

* System architecture diagram  
![ ](/public/assets/2021-07-25/becba7ad59a49a4aad30ff4db2cfafc4.png)

Custom model class Data layer, data presentation layer, data organization layer implementation  
First understand the following concepts:  
The architecture diagram in the project is used to define the module interface  
The class diagram in the project is used to define the interface of specific functions  
The flowchart in the engineering drawing is used to define the interaction between class objects  
After the module is implemented, unit testing is required

* `DataSource`Class design and implementation  
--- Set data source and read data  
--- parse the data to generate a data object  
![ ](/public/assets/2021-07-25/78f269b5dadf208f05ae7189bf3ff46f.png)
* `ScoreInfo` Class design and implementation:  
--- a complete set of data in the package data source  
--- Provides interface functions that return specific data values  
![ ](/public/assets/2021-07-25/44a509d8b2274d7db926ddb6fabdf8fd.png)
* `ScoreInfoModel`Class design and implementation:  
--- Use standard model classes`QStandardItemModel`As a member  
--- to`ScoreInfo`Class object is the smallest unit for data organization  
![ ](/public/assets/2021-07-25/39d3a0263abaa30d1f78c06bec8c2a87.png)  
![ ](/public/assets/2021-07-25/cdc72d334ea408c38028537975b67bea.png)