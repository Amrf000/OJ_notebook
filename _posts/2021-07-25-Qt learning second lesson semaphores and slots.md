---
layout: post
title: Qt learning second lesson semaphores and slots
category: qt5
tags: [qt5]
---
# Qt signals and slots
The signal slot is one of the mechanisms that the Qt framework is proud of. The so-called signal slot is actually the observer mode.After an event, For example, the button detects that it has been clicked,It will send out a signal (signal). This kind of transmission is purposeless, similar to broadcasting.If an object is interested in this signal, it will use the connect function,meaning is,Will wantProcessed signal andA function of its own (called slot) is bound to handle this signal. In other words,When the signal is sent, the connected slot function will automatically be called back. This is similar to the observer mode: when an event of interest occurs, an operation will be automatically triggered.
### 1\. The system's own signals and slots
First of all, we write a button in the empty form to achieve the function of clicking this button and the form is closed.
#include "mywidget.h"
#include<QPushButton>
3. MyWidget::MyWidget(QWidget *parent)
}: QWidget(parent)
{
}/* Another format for creating buttons
}QPushButton* btn = new QPushButton;
}btn->setParent(this);
}btn->setText("Glory of the King");
}btn->move(100,100);*/
}QPushButton* btn2 = new QPushButton("Close Window",this);
}this->resize(600,400);
13. }this->setWindowTitle("First item");
}this->setFixedSize(600,400);
}connect(btn2, &QPushButton::clicked, this, &MyWidget::close);//Connect the click event of btn2 with the close function of the form
}
}MyWidget::~MyWidget()
{
21. }
Functions connecting signals and slots:
connect(sender, signal, receiver, slot);
Sender: The person who sends the signal
Signal: The signal sent by the object
Receiver: Receive the object's signal
Slot: The function (slot) that the receiving object needs to call when receiving the signal
So Qt comes with a lot of signals and slots, how to find them?
This requires the use of the help document. In the help document, such as the click signal of our button above, enter QPushButton in the help document. First, we can look for the keyword Signals in Contents, the meaning of signals, but we found that we did not find it. At this time, we should think that maybe this signal is inherited by the parent class, so we can find the keyword in his parent class QAbstractButton, click the signals index to the signal that comes with the system as follows
![](https://img-blog.csdnimg.cn/20200331121207330.png)
The clicked here is what we want to find. The slot function is found in the same way as the signal, except that its keyword is slot.
![](https://img-blog.csdnimg.cn/20200331121611427.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0R1YW5ZaTE5OTg=,size_16,color_FFFFFF,t_70)
### 2\. Custom signals and slots
The use of connect() allows us to connect the signals and slots provided by the system. But Qt's signal and slot mechanism does not only use the part provided by the system, but also allows us to design our own signals and slots.
Now write a small example of custom signals and slots.
Create an example of a student and a teacher. After class, the teacher sends a hungry signal, and the student prints the string "Teacher, I'm eating"
First create a teacher class and a student class, both of which inherit the QObject object.
Then the teacher class declares a hungry signal,
![](https://img-blog.csdnimg.cn/20200331144300543.png)
The student class declares a treat() function for processing,
![](https://img-blog.csdnimg.cn/20200331144346498.png)
The signal does not need to be implemented, the slot function needs to be implemented.
![](https://img-blog.csdnimg.cn/2020033114442569.png)
Then in the Widget window class, new a teacher class and a student class, and set the parent window as the Widget window class.
Next, start connecting signals and slot functions.
Then send a signal and observe the output result.
![](https://img-blog.csdnimg.cn/20200331144742133.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0R1YW5ZaTE5OTg=,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20200331144812284.png)