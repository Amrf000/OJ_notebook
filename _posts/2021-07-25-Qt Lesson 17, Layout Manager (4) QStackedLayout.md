---
layout: post
title: Qt Lesson 17, Layout Manager (4) QStackedLayout
category: qt5
tags: [qt5]
---
1\. The most special layout manager
* Stacked layout manager (`QStackedLayout`）  
--- All components are inPerpendicular to the screenManaged in the direction of  
--- every timeOnly one componentWill be displayed on the screen  
--- onlyTopmost componentWill be finally displayed  
![ ](/md_blog/public/assets/2021-07-25/c7e3f5b88cbc34161dbb71b4fd3dd926.png)
* Features of Stacked Layout Manager  
--- Consistent component sizeAnd full of the display area of ​​the parent component  
--- Cannot be nested directlyOther layout managers  
--- canFree switchComponents that need to be displayed  
--- every time and onlyShow a widget
* `QStackedLayout` Usage summary  
--- `int addWidget(QWidget* widget)`  
--- `QWidget* currentWidget()　　　　　　　　　　　　//Return to the topmost widget of the stack layout manager`  
--- `void setCurrentIndex(int index)`  
--- `int currentIndex()`  
The last two functions: freely switch which component should be displayed currently
Indirect nesting method:
    	QHBoxLayout* hlayout = new QHBoxLayout(); QWidget* widget = new QWidget(this); hlayout->addWidget(&Btn2); hlayout->addWidget(&Btn3); widget->setLayout(hlayout); layout->addWidget(widget); 
widget.h
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> class Widget : public QWidget { Q_OBJECT protected: QPushButton Btn1; QPushButton Btn2; QPushButton Btn3; QPushButton Btn4; void init(); public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
widget.cpp
    #include "Widget.h" #include <QStackedLayout> #include <QHBoxLayout> Widget::Widget(QWidget *parent): QWidget(parent), Btn1(this), Btn2(this), Btn3(this), Btn4(this) { init(); } void Widget::init() { QStackedLayout* layout = new QStackedLayout(); QHBoxLayout* hlayout = new QHBoxLayout(); QWidget* widget = new QWidget(this); Btn1.setText("1st Button"); Btn2.setText("2st Button"); Btn3.setText("3st Button"); Btn4.setText("Test Button 4: xiebs"); hlayout->addWidget(&Btn2); hlayout->addWidget(&Btn3); widget->setLayout(hlayout); layout->addWidget(&Btn1); layout->addWidget(widget); layout->addWidget(&Btn4); layout->setCurrentIndex(2); setLayout(layout); } Widget::~Widget() { } 
![ ](/md_blog/public/assets/2021-07-25/a2eea094e3c8ba0be3ec1b2dddba2092.png)
2\. The concept of timer
* Timer is a very important role in engineering development
* Timer is usedTrigger a message every certain time
* The timer message will eventually be converted into a function call
* In general:  
--- The timer will call the specified function at regular intervals
`QTimer` How to use:  
1\. Write timer message processing function  
2\. Create a timer object in the program  
3\. Connect timer message and message processing function  
4\. Set the timer interval and start timing
Function: layout()  
![ ](/md_blog/public/assets/2021-07-25/39c8f30bbdb2ebfc0bb03569fe173807.png)  
If it is a QLayout object, it returns a pointer of the QLayout type and supports coercive type conversion.
widget.h
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> class Widget : public QWidget { Q_OBJECT protected: QPushButton Btn1; QPushButton Btn2; QPushButton Btn3; QPushButton Btn4; void init(); protected slots: void Time_timeout(); public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
widget.cpp
    #include "Widget.h" #include <QStackedLayout> #include <QHBoxLayout> #include <QTimer> #include <QDebug> Widget::Widget(QWidget *parent): QWidget(parent), Btn1(this), Btn2(this), Btn3(this), Btn4(this) { init(); } void Widget::init() { QStackedLayout* layout = new QStackedLayout(); QHBoxLayout* hlayout = new QHBoxLayout(); QWidget* widget = new QWidget(this); Btn1.setText("1st Button"); Btn2.setText("2st Button"); Btn3.setText("3st Button"); Btn4.setText("Test Button 4: xiebs"); hlayout->addWidget(&Btn2); hlayout->addWidget(&Btn3); widget->setLayout(hlayout); layout->addWidget(&Btn1); layout->addWidget(widget); layout->addWidget(&Btn4); layout->setCurrentIndex(0); setLayout(layout); QTimer *timer = new QTimer(this); connect(timer, SIGNAL(timeout()), this, SLOT(Time_timeout())); timer->start(1000); } void Widget::Time_timeout() { QStackedLayout* sLayout = dynamic_cast<QStackedLayout*>(layout()); if(sLayout != nullptr) { int index = (sLayout->currentIndex()+1)%(sLayout->count()); sLayout->setCurrentIndex(index); } } Widget::~Widget() { } 
![ ](/md_blog/public/assets/2021-07-25/2f2ef94ba1dc218f2f03cc9f2a070504.png)  
![ ](/md_blog/public/assets/2021-07-25/5a9271c71cb25444a7a3e4b0c383fd1a.png)  
![ ](/md_blog/public/assets/2021-07-25/5da007376f828ff87253ba377f5b243e.png)
* summary  
--- `QStackedLayout` Manage interface components in a stack  
--- `QStackedLayout` At most one component in the display  
--- `QStackedLayout` You can freely switch the components that need to be displayed  
--- `QTimer` Is the timer component in Qt  
--- `QTimer` Ability to trigger messages at specified time intervals
