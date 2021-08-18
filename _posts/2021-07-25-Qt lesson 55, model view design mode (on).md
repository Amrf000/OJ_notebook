---
layout: post
title: Qt lesson 55, model view design mode (on)
category: qt5
tags: [qt5]
---
* The core idea of ​​the model view design pattern:  
--- Model (data) and view (display) are separated  
--- The model provides a standard interface to access data externally (does not care how the data is displayed)  
--- View custom data display mode (do not care how the data is organized and stored)
* Intuitive understanding of model view mode:  
![ ](/md_blog/public/assets/2021-07-25/a812fac3b14bd2568b0074f9a04d3e60.png)
* The working mechanism of the model view mode:  
--- When the data changes: the model signals the view  
--- When the user interacts with the view: the view sends a signal to provide interactive information
* Model class hierarchy in Qt:  
![ ](/md_blog/public/assets/2021-07-25/ce6f3b7d849a40611e39a713d415d51f.png)
* The hierarchy of view classes in Qt:  
![ ](/md_blog/public/assets/2021-07-25/bd8fb6c7c7b4a6f1078e3c46102cdb9c.png)
* Key technical question: How does the model provide a unified way of accessing data?
In-depth understanding: In Qt, no matter what structure the model organizes the data, it must provide a unique index for each data;The view accesses the specific data in the model through the index。
Model view programming example:  
![ ](/md_blog/public/assets/2021-07-25/39a5a718da6356b47b84f2be27f20f74.png)
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QFileSystemModel> #include <QTreeView> class Widget : public QWidget { Q_OBJECT QFileSystemModel m_fsModel; QTreeView m_treeModel; public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
    #include "Widget.h" #include <QDir> Widget::Widget(QWidget *parent) : QWidget(parent) { m_treeModel.setParent(this); m_treeModel.move(10, 10); m_treeModel.resize(800, 500); m_fsModel.setRootPath(QDir::currentPath()); m_treeModel.setModel(&m_fsModel); m_treeModel.setRootIndex(m_fsModel.index(QDir::currentPath())); } Widget::~Widget() { } 
    #include "Widget.h" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); Widget w; w.show(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/20fc3de55b2320f451d117cbcb878b0a.png)  
summary:
* Model defines standard interface (member function) to access data
* The view obtains data through a standard interface and defines the display mode
* The model uses signals and slots to notify changes in view data
* Model data is represented in a hierarchical structure
