---
layout: post
title: Qt Lesson 2, Coordinate System in Qt
category: qt5
tags: [qt5]
---
* 1\. Coordinate system
* Positioning type  
--- positioning of top-level widgets  
--- positioning of parts in the window  
--- Widget size setting
2\. Coordinate system member functions in the QWidget class(Cross-platform)
    — x() 			//The horizontal coordinate of the starting point of the border — y()			//The vertical coordinate of the starting point of the border — width()		//The abscissa of the end of the client area — height()		//The ordinate of the end of the client area — geometry()	//Customer area x(),y(),width(),height() — frameGeometry()	//frame x(),y(),width(),height() 
![ ](/md_blog/public/assets/2021-07-25/555b9fa5ca52162e9bcbc5208c3fdeb4.png)  
Note:`geometry()` with `frameGeometry()` The geometric data in must be`show()`It is only valid after being called.  
`resize()` Function correspondence`width()` with `height()` Value of  
`move()` Function correspondence`x()` with `y()`Value of
    #include "Widget.h" #include "QDebug" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); Widget w; w.move(100,100); w.resize(400,300); w.show(); qDebug() << "QWidget::"; qDebug() << w.x(); qDebug() << w.y(); qDebug() << w.width(); qDebug() << w.height() << endl; qDebug() << "QWidget::geometry"; qDebug() << w.geometry().x(); qDebug() << w.geometry().y(); qDebug() << w.geometry().width(); qDebug() << w.geometry().height() << endl; qDebug() << "QWidget::frameGeometry"; qDebug() << w.frameGeometry().x(); qDebug() << w.frameGeometry().y(); qDebug() << w.frameGeometry().width(); qDebug() << w.frameGeometry().height() << endl; return a.exec(); }
