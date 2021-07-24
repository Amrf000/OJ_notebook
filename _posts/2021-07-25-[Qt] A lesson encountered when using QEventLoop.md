---
layout: post
title: [Qt] A lesson encountered when using QEventLoop
category: qt5
tags: [qt5]
---
##### 1, the problem description
The pseudo code is as follows:
    QEventLoop eventLoop; QObject::connect(this, &Class::signal, [](){ 	doSomething(); 	eventLoop.exit(0); }); emit signal(); eventLoop.exec(); 
When you execute eventLoop.exec(), it never causes you to quit.
##### 2, the cause analysis
I intend to execute doSomething() in the slot function before continuing. But after the signal is issued, the exit(0) function in the slot function is executed first, and the eventLoop.exec() is executed later, but there is no exit() to terminate the eventLoop, so that the following code will never be executed. carried out.
Remember: Exec() after exec(), the lesson of blood!