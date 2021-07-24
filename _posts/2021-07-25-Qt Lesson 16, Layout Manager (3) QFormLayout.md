---
layout: post
title: Qt Lesson 16, Layout Manager (3) QFormLayout
category: qt5
tags: [qt5]
---
Thinking:  
How to design the following user graphical interface?  
![ ](/public/assets/2021-07-25/9ffb7a1e312fdc0112fb83960fae6f3c.png)

* solution  
--- The coordinates and size of the absolutely positioned component  
--- Nested`QBoxLayout`  
--- Create 3 \* 2`QGridLayout`  
![ ](/public/assets/2021-07-25/619a4f6839f01dbea45e7361a0ab3b78.png)

widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> #include <QLabel> #include <QLineEdit> class Widget : public QWidget { Q_OBJECT protected: QLabel Namelabel; QLabel Emaillabel; QLabel Addresslabel; QLineEdit Nameedit; QLineEdit Emailedit; QLineEdit Addressedit; public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
    

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

widget.cpp
    
    #include "Widget.h" #include <QGridLayout> Widget::Widget(QWidget *parent): QWidget(parent), Namelabel(this), Emaillabel(this), Addresslabel(this), Nameedit(this), Emailedit(this), Addressedit(this) { QGridLayout* layout = new QGridLayout(this); Namelabel.setText("Name: "); Emaillabel.setText("Email: "); Addresslabel.setText("Address: "); layout->setSpacing(10); layout->addWidget(&Namelabel, 0, 0); layout->addWidget(&Nameedit, 0, 1); layout->addWidget(&Emaillabel, 1, 0); layout->addWidget(&Emailedit, 1, 1); layout->addWidget(&Addresslabel, 2, 0); layout->addWidget(&Addressedit, 2, 1); layout->setColumnStretch(0, 1); layout->setColumnStretch(1, 4); setLayout(layout); setWindowTitle("FTP"); } Widget::~Widget() { } 
    

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

Disadvantages: not beautiful enough after being pulled up  
![ ](/public/assets/2021-07-25/0cbf66d26679bf99bfc97c1d06a41615.png)

1、`QFormLayout` Layout manager

--- TakeFormWay to manage interface components  
--- Form layoutmiddlelabelwithComponentYesCorrespondenceRelationship  
![ ](/public/assets/2021-07-25/3fcbecceeba545e5f8442d7f8612db87.png)

* `QFormLayout`Usage summary  
![ ](/public/assets/2021-07-25/21d2f23b421ec7d72f52924e8808ac5b.png)  
form layoutSupport nesting, Other layout managers can be managed as sub-layouts.
* `QFormLayout` Style function  
--- `void setRowWrapPolicy(RowWrapPolicy policy)`　　　　　　//Line packing arrangement  
--- `void setLabelAlignment(Qt::Aligment alignment)`　　　　　//Label alignment strategy, specify how the label is aligned

widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> class Widget : public QWidget { Q_OBJECT public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
    

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

widget.cpp
    
    #include "Widget.h" #include <QLabel> #include <QLineEdit> #include <QFormLayout> Widget::Widget(QWidget *parent): QWidget(parent, Qt::WindowCloseButtonHint) { QFormLayout* layout = new QFormLayout(this); QLabel* Namelabel = new QLabel("Name:"); QLabel* Emaillabel = new QLabel("Email:"); QLabel* Addresslabel = new QLabel("Address:"); QLineEdit* Nameedit = new QLineEdit(this); QLineEdit* Emailedit = new QLineEdit(this); QLineEdit* Addressedit = new QLineEdit(this); layout->addRow(Namelabel, Nameedit); layout->addRow(Emaillabel, Emailedit); layout->addRow(Addresslabel, Addressedit); layout->setSpacing(10); layout->setRowWrapPolicy(QFormLayout::WrapAllRows); layout->setLabelAlignment(Qt::AlignRight); //Label right aligned setLayout(layout); } Widget::~Widget() { } 
    

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

* Layout manager nesting  
![ ](/public/assets/2021-07-25/c8df0c28ce6b86209df422c32febce16.png)

widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> class Widget : public QWidget { Q_OBJECT public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
    

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

widget.cpp
    
    #include "Widget.h" #include <QLabel> #include <QLineEdit> #include <QFormLayout> #include <QBoxLayout> Widget::Widget(QWidget *parent) : QWidget(parent) { QFormLayout* layout = new QFormLayout(); QVBoxLayout* layout1 = new QVBoxLayout(); QLineEdit* edit1 = new QLineEdit(); QLineEdit* edit2 = new QLineEdit(); layout1->addWidget(edit1); layout1->addWidget(edit2); QLineEdit* edit3 = new QLineEdit(); layout->addRow("Name:", edit3); layout->addRow("Email:", layout1); setLayout(layout); } Widget::~Widget() { } 
    

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

![ ](/public/assets/2021-07-25/b37987661b089ddc73ad433b141df237.png)

* summary  
--- `QFormLayout` Manage interface components in the form of a form  
--- `QFormLayout`The style is concise and clear  
--- `QFormLayout`Support the nesting of layout managers  
--- `QFormLayout`It is the most common layout method in embedded products