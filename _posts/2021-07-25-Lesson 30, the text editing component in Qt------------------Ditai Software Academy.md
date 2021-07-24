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
#include "MainWindow.h"
}MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent),
}lineEdit(this), plainEdit(this), textEdit(this)
{
}resize(600, 420);
7. }lineEdit.move(20, 20);
}lineEdit.resize(560, 100);
}lineEdit.insert("QLineEdit");
}lineEdit.insert("\n");
}lineEdit.insert("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
13. }plainEdit.move(20, 130);
}plainEdit.resize(560, 130);
}plainEdit.insertPlainText("QPlainTextEdit");
}plainEdit.insertPlainText("\n");
}plainEdit.insertPlainText("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
19. }textEdit.move(20, 270);
}textEdit.resize(560, 130);
}textEdit.insertPlainText("QTextEdit");
}textEdit.insertPlainText("\n");
}textEdit.insertHtml("<img src=\"C:\\Users\\hp\\Desktop\\D.T.png\" />");
}
}MainWindow::~MainWindow()
{
29. }
31. MainWindow.cpp
2、NopePad：
![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.h
1. #ifndef MAINWINDOW_H
2. #define MAINWINDOW_H
#include <QMenuBar>
#include <QMenu>
#include <QAction>
#include <QString>
#include <QtGui/QMainWindow>
#include <QToolBar>
#include <QIcon>
#include <QSize>
1#include <QStatusBar>
#include <QLabel>
#include <QPlainTextEdit>
14. class MainWindow : public QMainWindow
{
}Q_OBJECT
17. private:
}QPlainTextEdit mainEdit;
}QLabel statusLabel;
}MainWindow(QWidget *parent = 0);
}MainWindow(const MainWindow& obj);
}MainWindow* operator = (const MainWindow& obj);
}bool construct();
24. }bool initMenuBar();//Menu bar
}bool initToolBar();//Toolbar
}bool initStatusBar();//Status bar
}bool initinitMainEditor();//Edit window
29. }bool initFileMenu(QMenuBar* mb);//File menu
}bool initEditMenu(QMenuBar* mb);//Edit menu
}bool initFormatMenu(QMenuBar* mb);//Format menu
}bool initViewMenu(QMenuBar* mb);//View menu
}bool initHelpMenu(QMenuBar* mb);//Help menu
}bool initFileToolItem(QToolBar* tb);
36. }bool makeAction(QAction*& action, QString text, int ket);//menu item
}bool makeAction(QAction*& action, QString tip, QString icon);
39. public:
}static MainWindow* NewInstance();
}~MainWindow();
};
}#endif // MAINWINDOW_H
}MainWindow.h
![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.cpp
1. #ifndef MAINWINDOW_H
2. #define MAINWINDOW_H
#include <QMenuBar>
#include <QMenu>
#include <QAction>
#include <QString>
#include <QtGui/QMainWindow>
#include <QToolBar>
#include <QIcon>
#include <QSize>
1#include <QStatusBar>
#include <QLabel>
#include <QPlainTextEdit>
14. class MainWindow : public QMainWindow
{
}Q_OBJECT
17. private:
}QPlainTextEdit mainEdit;
}QLabel statusLabel;
}MainWindow(QWidget *parent = 0);
}MainWindow(const MainWindow& obj);
}MainWindow* operator = (const MainWindow& obj);
}bool construct();
24. }bool initMenuBar();//Menu bar
}bool initToolBar();//Toolbar
}bool initStatusBar();//Status bar
}bool initinitMainEditor();//Edit window
29. }bool initFileMenu(QMenuBar* mb);//File menu
}bool initEditMenu(QMenuBar* mb);//Edit menu
}bool initFormatMenu(QMenuBar* mb);//Format menu
}bool initViewMenu(QMenuBar* mb);//View menu
}bool initHelpMenu(QMenuBar* mb);//Help menu
}bool initFileToolItem(QToolBar* tb);
36. }bool makeAction(QAction*& action, QString text, int ket);//menu item
}bool makeAction(QAction*& action, QString tip, QString icon);
39. public:
}static MainWindow* NewInstance();
}~MainWindow();
};
}#endif // MAINWINDOW_H
45. MainWindow.h
![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) main.cpp
#include <QtGui/QApplication>
#include "MainWindow.h"
}int main(int argc, char *argv[])
{
}QApplication a(argc, argv);
}MainWindow* w = MainWindow::NewInstance();
}int ret = -1;
}if(w != NULL)
}{
}w->show();
}ret = a.exec();
}}
14. }delete w;
}return ret;
}
}main.cpp
# 2\. Summary
(1) Qt supports three commonly used text editing components
(2) The text editing component in Qt encapsulates commonly used editing functions
A, QLineEdit: single-line text editing component
B. QTextEdit: multi-line rich text editing component
C, QPlainTextEdit: multi-line ordinary text editing component