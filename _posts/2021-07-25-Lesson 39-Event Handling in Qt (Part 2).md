---
layout: post
title: Lesson 39-Event Handling in Qt (Part 2)
category: qt5
tags: [qt5]
---
# 

## 

##### 

### 

1\. Event processing in Qt

Event transmission process

![](/public/assets/2021-07-25/aa94b9de65954c1f24430768f3649567.png)

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
    

3. 4. #include <QtGui/QWidget>
    

5. #include "MyLineEdit.h"
    

6. 7. class Widget : public QWidget
    

8. {
    

9.  Q_OBJECT
    

10. 11.  MyLineEdit myLineEdit;
    

12. public:
    

13.  Widget(QWidget* parent = 0);
    

14.  bool event(QEvent* e);
    

15.  void keyPressEvent(QKeyEvent* e);
    

16.  ~Widget();
    

17. };
    

18. 19. #endif // WIDGET_H
    
    

Widget.cpp
    

1. #include "Widget.h"
    

2. #include <QDebug>
    

3. #include <QEvent>
    

4. 5. Widget::Widget(QWidget *parent)
    

6.  : QWidget(parent), myLineEdit(this)
    

7. {
    

8. 9. }
    

10. 11.  bool Widget::event(QEvent* e) //Qt events are handled by the event function
    

12. {
    

13.  if( e->type() == QEvent::KeyPress) //When the processed event is a key event
    

14.  {
    

15.  qDebug() << "Widget::event";
    

16.  }
    

17. 18.  return QWidget::event(e);//Call keyPressEvent() event handler function according to the type of event
    

19. }
    

20. 21.  void Widget::keyPressEvent(QKeyEvent* e)//Note that the event type is QKeyEvent
    

22. {
    

23.  qDebug() << "Widget::keyPressEvent";
    

24. 25.  QWidget::keyPressEvent(e);//Call the event handler function of the parent class
    

26. }
    

27. 28. Widget::~Widget()
    

29. {
    

30. 31. }
    
    

MyLineEdit.h
    

1. #ifndef MYLINEEDIT_H
    

2. #define MYLINEEDIT_H
    

3. 4. #include <QLineEdit>
    

5. 6. class MyLineEdit : public QLineEdit
    

7. {
    

8.  Q_OBJECT
    

9. public:
    

10.  explicit MyLineEdit(QWidget *parent = 0);
    

11.  bool event(QEvent* e);
    

12.  void keyPressEvent(QKeyEvent* e);
    

13. signals:
    

14. 15. public slots:
    

16. 17. };
    

18. 19. #endif // MYLINEEDIT_H
    
    

MyLineEdit.cpp
    

1. #include "MyLineEdit.h"
    

2. #include <QDebug>
    

3. #include <QEvent>
    

4. #include <QKeyEvent>
    

5. 6. MyLineEdit::MyLineEdit(QWidget *parent) :
    

7.  QLineEdit(parent)
    

8. {
    

9. }
    

10. 11. bool MyLineEdit::event(QEvent* e)
    

12. {
    

13.  if( e->type() == QEvent::KeyPress )
    

14.  {
    

15.  qDebug() << "MyLineEdit::event";
    

16.  }
    

17. 18.  return QLineEdit::event(e);
    

19. }
    

20. 21. void MyLineEdit::keyPressEvent(QKeyEvent* e)
    

22. {
    

23.  qDebug() << "MyLineEdit::keyPressEvent";
    

24. 25.  QLineEdit::keyPressEvent(e);
    

26. 27.  // e->ignore(); tells the Qt platform that the event has not been processed, it will call the parent component event function to process
    

28. }
    
    

main.cpp
    

1. #include <QtGui/QApplication>
    

2. #include "Widget.h"
    

3. 4. int main(int argc, char *argv[])
    

5. {
    

6.  QApplication a(argc, argv);
    

7.  Widget w;
    

8.  w.show();
    

9. 10.  return a.exec();
    

11. }
    
    

![](/public/assets/2021-07-25/d49a5013886944324bf3381241e1fa3e.gif)

Qt event is assigned to MyLineEdit, call its own event function for event processing

Calling different event processing functions according to different types of events.

When cancelled e-\>ignore();Annotate

![](/public/assets/2021-07-25/6b59f260f4a8e4e393b3d3ad111a6710.gif)

The event function of the parent component is called to handle the event

3\. Event processing in Qt

Event filter in Qt

--Event FilterCan monitor events received by other components

- ArbitraryQObjectAny objectUse as an event filter

- Event filter objectNeed to rewrite eventFilter() function

Passed by the monitored componentinstallEventFilter()letternumberInstall event filters

--Event FilterReceived an event before the component

--Event filters canDecide whether to forward the event to the component object

![](/public/assets/2021-07-25/0d443be009c3d06f02e236088c524c47.png)

Typical implementation of event filters

![](/public/assets/2021-07-25/dda7ccd0e2cf57eee9ab3aa209e0993d.png)

4\. Programming experiment

Use of event filters 39-2.pro

Widget.cpp (other code above)
    

1. #include "Widget.h"
    

2. #include <QDebug>
    

3. #include <QEvent>
    

4. #include <QKeyEvent>
    

5. 6. Widget::Widget(QWidget *parent)
    

7.  : QWidget(parent), myLineEdit(this)
    

8. {
    

9.  myLineEdit.installEventFilter(this);//The event filter installed by the monitored component
    

10. }
    

11. 12. bool Widget::event(QEvent* e)
    

13. {
    

14.  if( e->type() == QEvent::KeyPress )
    

15.  {
    

16.  qDebug() << "Widget::event";
    

17.  }
    

18. 19.  return QWidget::event(e);
    

20. }
    

21. 22. void Widget::keyPressEvent(QKeyEvent* e)
    

23. {
    

24.  qDebug() << "Widget::keyPressEvent";
    

25. 26.  QWidget::keyPressEvent(e);
    

27. }
    

28. 29.  bool Widget::eventFilter(QObject* obj, QEvent* e)//Event filter object rewrite eventFilter function
    

30. {
    

31.  bool ret = true;
    

32. 33.  if( (obj == &myLineEdit) && (e->type() == QEvent::KeyPress) )//When the monitored component is myLineEdit and the event is a key press
    

34.  {
    

35.  qDebug() << "Widget::eventFilter";
    

36. 37.  QKeyEvent* evt = dynamic_cast<QKeyEvent*>(e);
    

38. 39.  switch(evt->key())//When typing a number, the event is received normally by myLineEdit, all others are confiscated
    

40.  {
    

41.  case Qt::Key_0:
    

42.  case Qt::Key_1:
    

43.  case Qt::Key_2:
    

44.  case Qt::Key_3:
    

45.  case Qt::Key_4:
    

46.  case Qt::Key_5:
    

47.  case Qt::Key_6:
    

48.  case Qt::Key_7:
    

49.  case Qt::Key_8:
    

50.  case Qt::Key_9:
    

51.  ret = false;
    

52.  break;
    

53.  default:
    

54.  break;
    

55.  }
    

56.  }
    

57.  else
    

58.  {
    

59.  ret = QWidget::eventFilter(obj, e);
    

60.  }
    

61. 62.  return ret;
    

63. }
    

64. 65. Widget::~Widget()
    

66. {
    

67. 68. }
    
    

When pressing keys other than numbers

![](/public/assets/2021-07-25/3d740fcec5a1b460d8fa671cd53c74ea.gif)

â â â â â â ties â â â ¢ â â â â â ¢ â ¢ that the letters were found to be filtered, and the MyLineEdit object did not receive the time

When the number keys are pressed

![](/public/assets/2021-07-25/6cac8bd93eda7c676b3175fafff8f9cc.gif)

5\. Summary

Qt application hasStrict event processing sequence

After the Qt event is processedmayPass to parent component object

able to passinstallEventFilter()functionInstall event filters

Event filters canMonitor events received by other components

Event filters canDecide whether to forward the event to the component object