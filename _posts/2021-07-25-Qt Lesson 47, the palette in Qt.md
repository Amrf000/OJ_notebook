---
layout: post
title: Qt Lesson 47, the palette in Qt
category: qt5
tags: [qt5]
---
* 1\. The palette in Qt
* The QPalette class contains the color group of the component state
* The QPalette object mainly contains 3 state color descriptions  
--- Active color group (Active): the color scheme used by the component to gain focus  
--- Inactive color group (Inactive): the color scheme used when the component loses focus  
--- Disabled color group (Disabled): the color scheme used when the component is not available
* The color group in QPalette defines the color value of the group details
* `QPalette::ColorRole` Constant values ​​in are used to identify component details  
![ ](/md_blog/public/assets/2021-07-25/b70ace3636fcfce50c987384953584a3.png)
* Understanding the palette in Qt  
![ ](/md_blog/public/assets/2021-07-25/aaf3c6ce89d16370390b9a6a5ed58705.png)  
Understand:  
1\. The palette is a data structure for storing component color information  
2\. The colors used in the component appearance are all set in the palette
* How the palette is used
    QPalette p = widget.palette(); p.setColor(QPalette::Active, QPalette::WindowText, Qt::blue); p.setColor(QPalette::Inactive, QPalette::WindowText, Qt::blue); widget.setPalette(p); 
widget.h
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QLabel> #include <QLineEdit> #include <QPushButton> class Widget : public QWidget { Q_OBJECT protected: QLabel label; QLineEdit edit; QPushButton btn; protected slots: void onBtn_Clicked(); public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
widget.cpp
    #include "Widget.h" #include <QPalette> Widget::Widget(QWidget *parent): QWidget(parent), label(this), edit(this), btn(this) { label.move(20, 20); label.resize(120,40); label.setText("Text"); edit.move(20, 80); edit.resize(120,40); btn.move(20, 140); btn.resize(120,40); btn.setText("Text"); connect(&btn, SIGNAL(clicked()), this, SLOT(onBtn_Clicked())); QPalette p = btn.palette(); p.setColor(QPalette::Active, QPalette::ButtonText, Qt::red); p.setColor(QPalette::Inactive, QPalette::ButtonText, Qt::red); btn.setPalette(p); p = edit.palette(); p.setColor(QPalette::Active, QPalette::Highlight, Qt::blue); p.setColor(QPalette::Inactive, QPalette::HighlightedText, Qt::white); edit.setPalette(p); } void Widget::onBtn_Clicked() { QPalette p = label.palette(); p.setColor(QPalette::Active, QPalette::WindowText, Qt::green); p.setColor(QPalette::Inactive, QPalette::WindowText, Qt::green); label.setPalette(p); } Widget::~Widget() { } 
main.cpp
    #include "Widget.h" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); Widget w; w.show(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/0dcf8db4d8aebcdcd1351fd2c2d3a726.png)
Improvements in the text editor:
    bool MainWindow::initMainEditor() { bool ret = true; QPalette p = plainEdit.palette(); p.setColor(QPalette::Inactive, QPalette::Highlight, p.color(QPalette::Active, QPalette::Highlight)); p.setColor(QPalette::Inactive, QPalette::HighlightedText, p.color(QPalette::Active, QPalette::HighlightedText)); plainEdit.setPalette(p); } 
![ ](/md_blog/public/assets/2021-07-25/c9361bdd72df143da8c7d16dd3697645.png)  
Summary:
* QPalette is a data structure for identifying colors in Qt
* There are QPalette objects inside the window components
* Resetting the value of the component palette can change the color of a specific area
* QPalette object is an important role in customizing the appearance of components