---
layout: post
title: Qt Lesson 21, the status bar in the main window
category: qt5
tags: [qt5]
---
1\. The status bar in the main window
* The concept and meaning of the status bar  
--- The status bar is in the applicationOutput area for brief information  
--- Normal status barLocated at the very bottom of the main window  
--- The message type of the status bar  
　Real-time message: such as (current program status)  
　Permanent message: such as (program version number, organization name)  
　Progress message: such as (progress bar prompt, percentage prompt)
* Provide class components related to the status bar in Qt  
![ ](/md_blog/public/assets/2021-07-25/766d33f36badaaeb68318d420550946a.png)
* Create status bar in Qt main window  
![ ](/md_blog/public/assets/2021-07-25/5bf9002efcf6dd8f1721875baf9cc01f.png)
* Design principles of Qt status bar  
--- Left areaFor outputReal-time message  
--- Area on the rightFor settingPermanent message  
--- `addWidget` In the status barLeft halfAdd components  
--- `addPermanentWidget` In the status barRight halfAdd components
First experience of status bar:  
MainWindow.h
    #ifndef MAINWINDOW_H #define MAINWINDOW_H #include <QMainWindow> class MainWindow : public QMainWindow { Q_OBJECT public: MainWindow(QWidget *parent = nullptr); ~MainWindow(); }; #endif // MAINWINDOW_H 
MainWindow.cpp
    #include "MainWindow.h" #include <QStatusBar> #include <QLabel> #include <QLineEdit> #include <QPushButton> MainWindow::MainWindow(QWidget *parent): QMainWindow(parent) { QStatusBar* sb = statusBar(); QLabel* label = new QLabel("label"); QLineEdit* edit = new QLineEdit("edit"); QPushButton* btn = new QPushButton("btn"); sb->addPermanentWidget(label); sb->addPermanentWidget(edit); sb->addPermanentWidget(btn); sb->showMessage("xiebs"); } MainWindow::~MainWindow() { } 
main.cpp
    #include "MainWindow.h" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); MainWindow w; w.show(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/139a3bba8d1f496e532e26ee63607674.png)
* summary:  
--- The status bar is the area where brief information is output in the program  
--- `QStatusBar` Is the class for creating status bar components in Qt  
--- `QStatusBar` You can add any`QWidget`  
--- `QStatusBar` Has its own built-in design principles  
--- `QStatusBar` Various forms of status bar can be customized
