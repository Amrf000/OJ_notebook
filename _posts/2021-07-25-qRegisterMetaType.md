---
layout: post
title: qRegisterMetaType
category: qt5
tags: [qt5]
---
If you want to use a custom type in the Qt signal slot, you need to pay attention to registering the custom type with qRegisterMetaType. Of course, if you use the custom type signal/slot to pass without cross-threading, there may be no problem; once the cross-threading is involved It is very easy to make mistakes. Recall that the function of the signal slot is to communicate between the object and the object. It is inevitable to cross-thread. It is recommended to use the signal slot communication when using the custom type. It is best to use the qRegisterMetaType() to customize the type first. Register to avoid errors.
Summarize the use of qRegisterMetaType as follows:  
1\. Registration location: Before the first use of such a link cross-threaded signal/slot, it is generally registered in the constructor of the current class;  
2\. Registration method: At the top of the current class: \#include <QMetaType\>, add the code to the constructor: qRegisterMetaType<MyClass\>("Myclass");  
3\. The reference type of Myclass needs to be registered separately: qRegisterMetaType<MyClass\>("Myclass&");  
---------------------   
Author: Xue Ling Feng Yun  
Original: https://blog.csdn.net/u013360881/article/details/78878471
If it's a type defined by itself, if you want to use signal/slot to pass it, it's not that simple. If used directly, the following error will occur:
    QObject::connect: Cannot queue arguments of type 'TextAndNumber' (Make sure 'TextAndNumber' is registed using qRegisterMetaType().) 
Reason: When a signal is queued, its arguments are also put together in the queue (queued), which means that the parameters need to be copied before being transferred to the slot. Stored in the queue; in order to be able to store these arguments in the queue, Qt needs to construct, destruct, copy these objects, and in order for Qt to know how to do these things, the type of the parameter needs to use qRegisterMetaType Registration (as explained in the error message)
Step: (take the custom TextAndNumber type as an example)
Customize a type that contains at the top of this type: \#include <QMetaType\>
After the type definition is completed, add the declaration: Q\_DECLARE\_METATYPE(TextAndNumber);
Register this type in the main() function: qRegisterMetaType<TextAndNumber\>("TextAndNumber");
If you also want to use this type of reference, you can also register: qRegisterMetaType<TextAndNumber\>("TextAndNumber&");