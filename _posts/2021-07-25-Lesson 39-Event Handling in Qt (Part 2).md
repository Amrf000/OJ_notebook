---
layout: post
title: Lesson 39-Event Handling in Qt (Part 2)
category: qt5
tags: [qt5]
---
1\. Event processing in Qt
Event transmission process
![](/md_blog/public/assets/2021-07-25/aa94b9de65954c1f24430768f3649567.png)
After the event is processed by the component objectmayPass to itParent component object
Key member functions in QEvent
- void ignore(); 
RecipientIgnore the current event,Event may be passed to parent component
- void accept(); 
RecipientExpect to handle the current event (not absolute)
- bool isAccepted(); 
Determine whether the current event is processed 
2\. Programming experiment
Event processing sequence 39-1.pro
Widget.h
1. #ifndef WIDGET_H
2. #define WIDGET_H
3. #include <QtGui/QWidget>
#include "MyLineEdit.h"
}class Widget : public QWidget
{
}Q_OBJECT
10. }MyLineEdit myLineEdit;
12. public:
}Widget(QWidget* parent = 0);
}bool event(QEvent* e);
}void keyPressEvent(QKeyEvent* e);
}~Widget();
};
}#endif // WIDGET_H
Widget.cpp
#include "Widget.h"
#include <QDebug>
#include <QEvent>
}Widget::Widget(QWidget *parent)
}: QWidget(parent), myLineEdit(this)
{
8. }
10. }bool Widget::event(QEvent* e) //Qt events are handled by the event function
{
}if( e->type() == QEvent::KeyPress) //When the processed event is a key event
}{
}qDebug() << "Widget::event";
}}
17. }return QWidget::event(e);//Call keyPressEvent() event handler function according to the type of event
}
20. }void Widget::keyPressEvent(QKeyEvent* e)//Note that the event type is QKeyEvent
{
}qDebug() << "Widget::keyPressEvent";
24. }QWidget::keyPressEvent(e);//Call the event handler function of the parent class
}
}Widget::~Widget()
{
30. }
MyLineEdit.h
1. #ifndef MYLINEEDIT_H
2. #define MYLINEEDIT_H
3. #include <QLineEdit>
}class MyLineEdit : public QLineEdit
{
}Q_OBJECT
9. public:
}explicit MyLineEdit(QWidget *parent = 0);
}bool event(QEvent* e);
}void keyPressEvent(QKeyEvent* e);
13. signals:
}public slots:
16. };
}#endif // MYLINEEDIT_H
MyLineEdit.cpp
#include "MyLineEdit.h"
#include <QDebug>
#include <QEvent>
#include <QKeyEvent>
}MyLineEdit::MyLineEdit(QWidget *parent) :
}QLineEdit(parent)
{
}
}bool MyLineEdit::event(QEvent* e)
{
}if( e->type() == QEvent::KeyPress )
}{
}qDebug() << "MyLineEdit::event";
}}
17. }return QLineEdit::event(e);
}
}void MyLineEdit::keyPressEvent(QKeyEvent* e)
{
}qDebug() << "MyLineEdit::keyPressEvent";
24. }QLineEdit::keyPressEvent(e);
26. }// e->ignore(); tells the Qt platform that the event has not been processed, it will call the parent component event function to process
}
main.cpp
#include <QtGui/QApplication>
#include "Widget.h"
}int main(int argc, char *argv[])
{
}QApplication a(argc, argv);
}Widget w;
}w.show();
9. }return a.exec();
}
![](/md_blog/public/assets/2021-07-25/d49a5013886944324bf3381241e1fa3e.gif)
Qt event is assigned to MyLineEdit, call its own event function for event processing
Calling different event processing functions according to different types of events.
When cancelled e-\>ignore();Annotate
![](/md_blog/public/assets/2021-07-25/6b59f260f4a8e4e393b3d3ad111a6710.gif)
The event function of the parent component is called to handle the event
3\. Event processing in Qt
Event filter in Qt
--Event FilterCan monitor events received by other components
- ArbitraryQObjectAny objectUse as an event filter
- Event filter objectNeed to rewrite eventFilter() function
Passed by the monitored componentinstallEventFilter()letternumberInstall event filters
--Event FilterReceived an event before the component
--Event filters canDecide whether to forward the event to the component object
![](/md_blog/public/assets/2021-07-25/0d443be009c3d06f02e236088c524c47.png)
Typical implementation of event filters
![](/md_blog/public/assets/2021-07-25/dda7ccd0e2cf57eee9ab3aa209e0993d.png)
4\. Programming experiment
Use of event filters 39-2.pro
Widget.cpp (other code above)
#include "Widget.h"
#include <QDebug>
#include <QEvent>
#include <QKeyEvent>
}Widget::Widget(QWidget *parent)
}: QWidget(parent), myLineEdit(this)
{
}myLineEdit.installEventFilter(this);//The event filter installed by the monitored component
}
}bool Widget::event(QEvent* e)
{
}if( e->type() == QEvent::KeyPress )
}{
}qDebug() << "Widget::event";
}}
18. }return QWidget::event(e);
}
}void Widget::keyPressEvent(QKeyEvent* e)
{
}qDebug() << "Widget::keyPressEvent";
25. }QWidget::keyPressEvent(e);
}
28. }bool Widget::eventFilter(QObject* obj, QEvent* e)//Event filter object rewrite eventFilter function
{
}bool ret = true;
32. }if( (obj == &myLineEdit) && (e->type() == QEvent::KeyPress) )//When the monitored component is myLineEdit and the event is a key press
}{
}qDebug() << "Widget::eventFilter";
36. }QKeyEvent* evt = dynamic_cast<QKeyEvent*>(e);
38. }switch(evt->key())//When typing a number, the event is received normally by myLineEdit, all others are confiscated
}{
}case Qt::Key_0:
}case Qt::Key_1:
}case Qt::Key_2:
}case Qt::Key_3:
}case Qt::Key_4:
}case Qt::Key_5:
}case Qt::Key_6:
}case Qt::Key_7:
}case Qt::Key_8:
}case Qt::Key_9:
}ret = false;
}break;
}default:
}break;
}}
}}
}else
}{
}ret = QWidget::eventFilter(obj, e);
}}
61. }return ret;
}
}Widget::~Widget()
{
67. }
When pressing keys other than numbers
![](/md_blog/public/assets/2021-07-25/3d740fcec5a1b460d8fa671cd53c74ea.gif)
â â â â â â ties â â â ¢ â â â â â ¢ â ¢ that the letters were found to be filtered, and the MyLineEdit object did not receive the time
When the number keys are pressed
![](/md_blog/public/assets/2021-07-25/6cac8bd93eda7c676b3175fafff8f9cc.gif)
5\. Summary
Qt application hasStrict event processing sequence
After the Qt event is processedmayPass to parent component object
able to passinstallEventFilter()functionInstall event filters
Event filters canMonitor events received by other components
Event filters canDecide whether to forward the event to the component object