---
layout: post
title: Lesson 30, the text editing component in Qt
category: qt5
tags: [qt5]
---
# One, text editing component

1\. Qt supports three commonly used text editing components

(1) QLineEdit: single-line text editing component

(2) QTextEdit: multi-line rich text (with pictures, videos, etc.) editing component

(3) QPlainTextEdit: multi-line ordinary text editing component

2\. Inheritance hierarchy diagram of commonly used text editing components in Qt

![](/md_blog/public/assets/2021-07-25/b9b1d6f729f3fb663b2f94f1111231f4.png)

3\. Comparison of the characteristics of different text components

![](/md_blog/public/assets/2021-07-25/366e5035a2b7d0104ef896b676d91e21.png)

4\. Built-in functions of commonly used text editing components in Qt

![](/md_blog/public/assets/2021-07-25/48b1d18212e0562b27698afa51955f38.png)

1\. A preliminary exploration of text editing components

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.cpp
    

1. #include "MainWindow.h"
    

2. 3. MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent),
    

4.  lineEdit(this), plainEdit(this), textEdit(this)
    

5. {
    

6.  resize(600, 420);
    

7. 8.  lineEdit.move(20, 20);
    

9.  lineEdit.resize(560, 100);
    

10.  lineEdit.insert("QLineEdit");
    

11.  lineEdit.insert("\n");
    

12.  lineEdit.insert("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
    

13. 14.  plainEdit.move(20, 130);
    

15.  plainEdit.resize(560, 130);
    

16.  plainEdit.insertPlainText("QPlainTextEdit");
    

17.  plainEdit.insertPlainText("\n");
    

18.  plainEdit.insertPlainText("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
    

19. 20.  textEdit.move(20, 270);
    

21.  textEdit.resize(560, 130);
    

22.  textEdit.insertPlainText("QTextEdit");
    

23.  textEdit.insertPlainText("\n");
    

24.  textEdit.insertHtml("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
    

25. }
    

26. 27. MainWindow::~MainWindow()
    

28. {
    

29. 30. }
    

31. MainWindow.cpp
    
    

2、NopePad：

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.h
    

1. #ifndef MAINWINDOW_H
    

2. #define MAINWINDOW_H
    

3. #include <QMenuBar>
    

4. #include <QMenu>
    

5. #include <QAction>
    

6. #include <QString>
    

7. #include <QtGui/QMainWindow>
    

8. #include <QToolBar>
    

9. #include <QIcon>
    

10. #include <QSize>
    

11. #include <QStatusBar>
    

12. #include <QLabel>
    

13. #include <QPlainTextEdit>
    

14. class MainWindow : public QMainWindow
    

15. {
    

16.  Q_OBJECT
    

17. private:
    

18.  QPlainTextEdit mainEdit;
    

19.  QLabel statusLabel;
    

20.  MainWindow(QWidget *parent = 0);
    

21.  MainWindow(const MainWindow& obj);
    

22.  MainWindow* operator = (const MainWindow& obj);
    

23.  bool construct();
    

24. 25.  bool initMenuBar();//Menu bar
    

26.  bool initToolBar();//Toolbar
    

27.  bool initStatusBar();//Status bar
    

28.  bool initinitMainEditor();//Edit window
    

29. 30.  bool initFileMenu(QMenuBar* mb);//File menu
    

31.  bool initEditMenu(QMenuBar* mb);//Edit menu
    

32.  bool initFormatMenu(QMenuBar* mb);//Format menu
    

33.  bool initViewMenu(QMenuBar* mb);//View menu
    

34.  bool initHelpMenu(QMenuBar* mb);//Help menu
    

35.  bool initFileToolItem(QToolBar* tb);
    

36. 37.  bool makeAction(QAction*& action, QString text, int ket);//menu item
    

38.  bool makeAction(QAction*& action, QString tip, QString icon);
    

39. public:
    

40.  static MainWindow* NewInstance();
    

41.  ~MainWindow();
    

42. };
    

43. 44. #endif // MAINWINDOW_H
    

45. 46. MainWindow.h
    
    

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.cpp
    

1. #ifndef MAINWINDOW_H
    

2. #define MAINWINDOW_H
    

3. #include <QMenuBar>
    

4. #include <QMenu>
    

5. #include <QAction>
    

6. #include <QString>
    

7. #include <QtGui/QMainWindow>
    

8. #include <QToolBar>
    

9. #include <QIcon>
    

10. #include <QSize>
    

11. #include <QStatusBar>
    

12. #include <QLabel>
    

13. #include <QPlainTextEdit>
    

14. class MainWindow : public QMainWindow
    

15. {
    

16.  Q_OBJECT
    

17. private:
    

18.  QPlainTextEdit mainEdit;
    

19.  QLabel statusLabel;
    

20.  MainWindow(QWidget *parent = 0);
    

21.  MainWindow(const MainWindow& obj);
    

22.  MainWindow* operator = (const MainWindow& obj);
    

23.  bool construct();
    

24. 25.  bool initMenuBar();//Menu bar
    

26.  bool initToolBar();//Toolbar
    

27.  bool initStatusBar();//Status bar
    

28.  bool initinitMainEditor();//Edit window
    

29. 30.  bool initFileMenu(QMenuBar* mb);//File menu
    

31.  bool initEditMenu(QMenuBar* mb);//Edit menu
    

32.  bool initFormatMenu(QMenuBar* mb);//Format menu
    

33.  bool initViewMenu(QMenuBar* mb);//View menu
    

34.  bool initHelpMenu(QMenuBar* mb);//Help menu
    

35.  bool initFileToolItem(QToolBar* tb);
    

36. 37.  bool makeAction(QAction*& action, QString text, int ket);//menu item
    

38.  bool makeAction(QAction*& action, QString tip, QString icon);
    

39. public:
    

40.  static MainWindow* NewInstance();
    

41.  ~MainWindow();
    

42. };
    

43. 44. #endif // MAINWINDOW_H
    

45. MainWindow.h
    
    

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) main.cpp
    

1. #include <QtGui/QApplication>
    

2. #include "MainWindow.h"
    

3. 4. int main(int argc, char *argv[])
    

5. {
    

6.  QApplication a(argc, argv);
    

7.  MainWindow* w = MainWindow::NewInstance();
    

8.  int ret = -1;
    

9.  if(w != NULL)
    

10.  {
    

11.  w->show();
    

12.  ret = a.exec();
    

13.  }
    

14. 15.  delete w;
    

16.  return ret;
    

17. }
    

18. 19. main.cpp
    
    

# 2\. Summary

(1) Qt supports three commonly used text editing components

(2) The text editing component in Qt encapsulates commonly used editing functions

A, QLineEdit: single-line text editing component

B. QTextEdit: multi-line rich text editing component

C, QPlainTextEdit: multi-line ordinary text editing component