---
layout: post
title: Lesson 39-Event Handling in Qt (Part 2)
category: qt5
tags: [qt5]
---
1. Event processing in Qt
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
2. Programming experiment
Event processing sequence 39-1.pro
MyLineEdit.h
```
#ifndef MYLINEEDIT_H
#define MYLINEEDIT_H
#include <QLineEdit>

class MyLineEdit : public QLineEdit {

public:
  MyLineEdit(QWidget *parent = nullptr);
  bool event(QEvent *e);
  void keyPressEvent(QKeyEvent *e);
};

#endif // MYLINEEDIT_H
```
Widget.h
```
#ifndef WIDGET_H
#define WIDGET_H

#include "MyLineEdit.h"
#include <QWidget>

class Widget : public QWidget {
  Q_OBJECT
  MyLineEdit edit;

public:
  Widget(QWidget *parent = nullptr);

  bool event(QEvent *e);
  void keyPressEvent(QKeyEvent *e);

  ~Widget();
};
#endif // WIDGET_H
```
main.cpp
```
#include "Widget.h"

#include <QApplication>

int main(int argc, char *argv[]) {
  QApplication a(argc, argv);
  Widget w;
  w.show();
  return a.exec();
}
```
MyLineEdit.cpp
```
#include "MyLineEdit.h"
#include <QDebug>
#include <QEvent>
#include <QKeyEvent>

MyLineEdit::MyLineEdit(QWidget *parent) : QLineEdit(parent) {}

bool MyLineEdit::event(QEvent *e) {
  if (e->type() == QEvent::KeyPress) {
    qDebug() << "MyLineEdit::event";
  }
  return QLineEdit::event(e);
}

void MyLineEdit::keyPressEvent(QKeyEvent *e) {
  qDebug() << "MyLineEdit::keyPressEvent";
  QLineEdit::keyPressEvent(e);
  // e->ignore();            //If the ignore function is called, the event may
  // be passed to its parent component, where it is passed to the parent
  // component
} // What is the parent component, the line editing component is in the widget
  // window, then the widget window is the parent component of the line editing
  // component
```
Widget.cpp
```
#include "Widget.h"
#include <QDebug>
#include <QEvent>

Widget::Widget(QWidget *parent) : QWidget(parent), edit(this) {}

bool Widget::event(QEvent *e) {
  if (e->type() == QEvent::KeyPress) {
    qDebug() << "Widget::event";
  }

  return QWidget::event(e);
}

void Widget::keyPressEvent(QKeyEvent *e) {
  qDebug() << "Widget::keyPressEvent";
  QWidget::keyPressEvent(e);
}

Widget::~Widget() {}
```
![](/md_blog/public/assets/2021-07-25/d49a5013886944324bf3381241e1fa3e.gif)
Qt event is assigned to MyLineEdit, call its own event function for event processing
Calling different event processing functions according to different types of events.
When cancelled e->ignore();Annotate
![](/md_blog/public/assets/2021-07-25/6b59f260f4a8e4e393b3d3ad111a6710.gif)
The event function of the parent component is called to handle the event
3. Event processing in Qt
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
4. Programming experiment
Use of event filters 39-2.pro

MyLineEdit.h
```
#ifndef MYLINEEDIT_H
#define MYLINEEDIT_H
#include <QLineEdit>

class MyLineEdit : public QLineEdit {

public:
  MyLineEdit(QWidget *parent = nullptr);
  bool event(QEvent *e);
  void keyPressEvent(QKeyEvent *e);
};

#endif // MYLINEEDIT_H
```
Widget.h
```
#ifndef WIDGET_H
#define WIDGET_H

#include "MyLineEdit.h"
#include <QWidget>

class Widget : public QWidget {
  Q_OBJECT
  MyLineEdit edit;

public:
  Widget(QWidget *parent = nullptr);

  bool event(QEvent *e);
  void keyPressEvent(QKeyEvent *e);
  bool eventFilter(QObject *obj, QEvent *e);
  ~Widget();
};
#endif // WIDGET_H
```
main.cpp
```
#include "Widget.h"

#include <QApplication>

int main(int argc, char *argv[]) {
  QApplication a(argc, argv);
  Widget w;
  w.show();
  return a.exec();
}
```
MyLineEdit.cpp
```
#include "MyLineEdit.h"
#include <QDebug>
#include <QEvent>
#include <QKeyEvent>

MyLineEdit::MyLineEdit(QWidget *parent) : QLineEdit(parent) {}

bool MyLineEdit::event(QEvent *e) {
  if (e->type() == QEvent::KeyPress) {
    qDebug() << "MyLineEdit::event";
  }
  return QLineEdit::event(e);
}

void MyLineEdit::keyPressEvent(QKeyEvent *e) {
  qDebug() << "MyLineEdit::keyPressEvent";
  QLineEdit::keyPressEvent(e);
  // e->ignore();            //If the ignore function is called, the event may
  // be passed to its parent component, where it is passed to the parent
  // component
} // What is the parent component, the line editing component is in the widget
  // window, then the widget window is the parent component of the line editing
  // component
```
Widget.cpp (other code above)
```
#include "Widget.h"
#include <QDebug>
#include <QEvent>

Widget::Widget(QWidget *parent) : QWidget(parent), edit(this) {
  edit.installEventFilter(this); // Install event filter
}

bool Widget::event(QEvent *e) {
  if (e->type() == QEvent::KeyPress) {
    qDebug() << "Widget::event";
  }

  return QWidget::event(e);
}

void Widget::keyPressEvent(QKeyEvent *e) {
  qDebug() << "Widget::keyPressEvent";
  QWidget::keyPressEvent(e);
}

// Rewrite the event filter function. If the component is line editing and the
// event is a button, output statements, and only line editing can only output
// 0-9; otherwise, call the normal event filter function.
bool Widget::eventFilter(QObject *obj, QEvent *e) {
  bool ret = true;
  if ((obj == &edit) && (e->type() == QEvent::KeyPress)) {
    qDebug() << "Widget::eventFilter";
    QKeyEvent *evt = dynamic_cast<QKeyEvent *>(e);

    switch (evt->key()) {
    case Qt::Key_0:
    case Qt::Key_1:
    case Qt::Key_2:
    case Qt::Key_3:
    case Qt::Key_4:
    case Qt::Key_5:
    case Qt::Key_6:
    case Qt::Key_7:
    case Qt::Key_8:
    case Qt::Key_9:
      ret = false;
      break;
    default:
      break;
    }
  } else {
    ret = QWidget::eventFilter(obj, e);
  }
  return ret;
}

Widget::~Widget() {}
```
When pressing keys other than numbers
![](/md_blog/public/assets/2021-07-25/3d740fcec5a1b460d8fa671cd53c74ea.gif)
â â â â â â ties â â â ¢ â â â â â ¢ â ¢ that the letters were found to be filtered, and the MyLineEdit object did not receive the time
When the number keys are pressed
![](/md_blog/public/assets/2021-07-25/6cac8bd93eda7c676b3175fafff8f9cc.gif)
5. Summary
Qt application hasStrict event processing sequence
After the Qt event is processedmayPass to parent component object
able to passinstallEventFilter()functionInstall event filters
Event filters canMonitor events received by other components
Event filters canDecide whether to forward the event to the component object
