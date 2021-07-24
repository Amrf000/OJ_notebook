---
layout: post
title: Qt lesson 12, standard dialog box (medium) color, input in Qt
category: qt5
tags: [qt5]
---
# 

## 

* 1\. Color dialog

* Qt provides a predefined color dialog box QColorDialog class
* The QColorDialog class is used to provide dialog components with specified colors  
![ ](/public/assets/2021-07-25/54e16bc3d9d7e46c14450ff1d818c9fb.png)
* How to use the color dialog  
![ ](/public/assets/2021-07-25/c8658c1b9475477aad09750e2e998788.png)
* The QColor class in Qt is used to represent the concept of color in the program
* The QColor class supports multiple color expressions at the same time  
--- RGB: Three-color model based on red, green and blue  
--- HSV: Hexagonal cone model based on hue, saturation and lightness  
--- CMKY: Full-color printing color model based on sky blue, magenta, yellow, and black

program:

Widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> #include <QDebug> class Widget : public QWidget { Q_OBJECT private: QPushButton ColorBtn; QPushButton InputBtn; private slots: void ColorBtn_Clicked(); void InputBtn_Clicked(); public: explicit Widget(QWidget *parent = 0); signals: }; #endif 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

Widget.cpp
    
    #include "Widget.h" #include <QColorDialog> Widget::Widget(QWidget *parent) : QWidget(parent), ColorBtn(this),InputBtn(this) { ColorBtn.setText("Color Dialog"); ColorBtn.move(20,20); ColorBtn.resize(140,30); InputBtn.setText("Input Dialog"); InputBtn.move(20,70); InputBtn.resize(140,30); setFixedSize(180,120); connect(&ColorBtn,SIGNAL(clicked()),this,SLOT(ColorBtn_Clicked())); connect(&InputBtn,SIGNAL(clicked()),this,SLOT(InputBtn_Clicked())); } void Widget::ColorBtn_Clicked() { QColorDialog dialog; dialog.setWindowTitle("Color Editor"); dialog.setCurrentColor(QColor(100,111,222)); //dialog.setCurrentColor(Qt::red); if(dialog.exec() == QColorDialog::Accepted) { //qDebug() << dialog.selectedColor(); QColor color = dialog.selectedColor(); qDebug() << color; qDebug() << color.red(); qDebug() << color.green(); qDebug() << color.blue(); qDebug() << color.hue(); qDebug() << color.saturation(); qDebug() << color.value(); } } void Widget::InputBtn_Clicked() { } 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

* 26

* 27

* 28

* 29

* 30

* 31

* 32

* 33

* 34

* 35

* 36

* 37

* 38

* 39

* 40

* 41

* 42

* 43

* 44

* 45

* 46

* 47

main.cpp
    
    #include "Widget.h" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); Widget w; w.show(); return a.exec(); } 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

![ ](/public/assets/2021-07-25/1ff1677a8fe5fca0881508e4643eb211.png)  
![ ](/public/assets/2021-07-25/a03f5e0d045979bd0f9f45d3e32ac788.png)

* Utility functions in QColorDialog  
--- `QColorDialog::getColor`

A modal color dialog box with a specified window title pops up (select a color if it is not specified), allowing the user to select a color and return the color. The color is initially set to initial. The dialog is a child dialog of the parent dialog. If the user cancels the dialog box, it will return an invalid color (see`QColor::isValid()`)。
    
    void Widget::ColorBtn_Clicked() { QColor color = QColorDialog::getColor(Qt::white, this, "Color Editor", QColorDialog::DontUseNativeDialog); if(color.isValid() == true) { qDebug() << color; qDebug() << color.red(); qDebug() << color.green(); qDebug() << color.blue(); qDebug() << color.hue(); qDebug() << color.saturation(); qDebug() << color.value(); } } 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

2\. Input dialog box

* Qt provides a predefined input dialog QInputDialog class
* The QInputDialog class is used where temporary data input is required  
![ ](/public/assets/2021-07-25/53ba193e7e18a639662a5610f0581ed2.png)
* How to use the input dialog  
![ ](/public/assets/2021-07-25/8128da80107d769e7d5ccede79ebe343.png)
* Input mode of the input dialog
    
    QInputDialog::TextInput — input a text string QInputDialog::IntInput — input an integer QInputDialog::DoubleInput — input floating point numbers qDebug() << dlg.textValue(); qDebug() << dlg.intValue(); qDebug() << dlg.doubleValue(); 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

    void Widget::InputBtn_Clicked() { // QInputDialog dlg; // dlg.setWindowTitle("Input Edit"); // dlg.setLabelText("Please enter an integer"); // dlg.setInputMode(QInputDialog::IntInput); // dlg.setIntMinimum(0); // dlg.setIntMaximum(255); // if(dlg.exec() == QInputDialog::Accepted) // { // qDebug() << dlg.intValue(); // } QInputDialog dlg; dlg.setWindowTitle("Input Edit"); dlg.setLabelText("Please enter an Text"); dlg.setInputMode(QInputDialog::TextInput); if(dlg.exec() == QInputDialog::Accepted) { qDebug() << dlg.textValue(); } } 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

* Utility functions in QInputDialog
    
    QInputDialog::getDouble QInputDialog::getInt QInputDialog::getItem QInputDialog::getText 
    

* 1

* 2

* 3

* 4

* summary  
--- The QColorDialog class is used to provide dialog components with specified colors  
--- QColor class is used to represent the concept of color in the program  
--- The QInputDialog class is used for occasions that require temporary data input