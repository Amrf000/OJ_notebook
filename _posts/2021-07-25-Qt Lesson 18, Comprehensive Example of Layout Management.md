---
layout: post
title: Qt Lesson 18, Comprehensive Example of Layout Management
category: qt5
tags: [qt5]
---
# 

## 

##### 

### 

* Requirements analysis: (practice developing a wizard user interface)  
--- display different wizard pages on the same interface  
--- passPrevious with Next step Button to switch  
--- Element components and component arrangements on different pages are different  
--- components on the page are arranged through the layout manager
* Solution (interface design through layout nesting)  
In fact, this kind of thing has only one page, just through`QStackedLayout`This page layout uses slot functions to switch pages.  
![ ](/md_blog/public/assets/2021-07-25/3cb0976d9807f6cac14c6561f41a556a.png)
* Through`QStackLayout` Manage different pages  
![ ](/md_blog/public/assets/2021-07-25/cf82d5d19ded5da8167fe475e0a3c19e.png)
* Generate different pages through subcomponents  
![ ](/md_blog/public/assets/2021-07-25/c748d8f83578844b11b934d5df1f8ca3.png)

widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> #include <QLabel> #include <QLineEdit> #include <QStackedLayout> class Widget : public QWidget { Q_OBJECT private: QStackedLayout slayout; QPushButton PreBtn; QPushButton NextBtn; QLabel label1; QLabel label2; QLabel label3; QLabel label4; QLineEdit edit; QPushButton btn1; QPushButton btn2; void initControl(); QWidget* get1stPage(); QWidget* get2ndPage(); QWidget* get3rdPage(); private slots: void PreBtnClicked(); void NextBtnClicked(); public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif // WIDGET_H 
    

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

widget.cpp
    
    #include "Widget.h" #include <QVBoxLayout> #include <QHBoxLayout> #include <QGridLayout> #include <QFormLayout> #include <QStackedLayout> #include <QDebug> Widget::Widget(QWidget *parent): QWidget(parent) { initControl(); } void Widget::initControl() { QVBoxLayout* vlayout = new QVBoxLayout(); QHBoxLayout* hlayout = new QHBoxLayout(); PreBtn.setText("Pre Page"); PreBtn.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Fixed); PreBtn.setMinimumSize(120, 30); NextBtn.setText("Next Page"); NextBtn.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Fixed); NextBtn.setMinimumSize(120, 30); connect(&PreBtn, SIGNAL(clicked()), this, SLOT(PreBtnClicked())); connect(&NextBtn, SIGNAL(clicked()), this, SLOT(NextBtnClicked())); hlayout->addWidget(&PreBtn); hlayout->addWidget(&NextBtn); slayout.addWidget(get1stPage()); slayout.addWidget(get2ndPage()); slayout.addWidget(get3rdPage()); vlayout->addLayout(&slayout); vlayout->addLayout(hlayout); setLayout(vlayout); } QWidget* Widget::get1stPage() { QWidget* ret = new QWidget(); QGridLayout* layout = new QGridLayout(); label1.setText("This"); label2.setText("is"); label3.setText("1st"); label4.setText("page"); layout->addWidget(&label1, 0, 0); layout->addWidget(&label2, 0, 1); layout->addWidget(&label3, 1, 0); layout->addWidget(&label4, 1, 1); qDebug() << ret; qDebug() << label1.parent(); qDebug() << label2.parent(); qDebug() << label3.parent(); qDebug() << label4.parent(); ret->setLayout(layout); qDebug() << ret; qDebug() << label1.parent(); qDebug() << label2.parent(); qDebug() << label3.parent(); qDebug() << label4.parent(); return ret; } QWidget* Widget::get2ndPage() { QWidget* ret = new QWidget(); QFormLayout* layout = new QFormLayout(); edit.setText("This is 2nd page"); layout->addRow("Hint:", &edit); ret->setLayout(layout); return ret; } QWidget* Widget::get3rdPage() { QWidget* ret = new QWidget(); QVBoxLayout* layout = new QVBoxLayout(); btn1.setText("This is"); btn2.setText("3rd page"); layout->addWidget(&btn1); layout->addWidget(&btn2); ret->setLayout(layout); return ret; } void Widget::PreBtnClicked() { int index = (slayout.currentIndex()-1+3) % 3; slayout.setCurrentIndex(index); } void Widget::NextBtnClicked() { int index = (slayout.currentIndex()+1) % 3; slayout.setCurrentIndex(index); } Widget::~Widget() { } 
    

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

* 48

* 49

* 50

* 51

* 52

* 53

* 54

* 55

* 56

* 57

* 58

* 59

* 60

* 61

* 62

* 63

* 64

* 65

* 66

* 67

* 68

* 69

* 70

* 71

* 72

* 73

* 74

* 75

* 76

* 77

* 78

* 79

* 80

* 81

* 82

* 83

* 84

* 85

* 86

* 87

* 88

* 89

* 90

* 91

* 92

* 93

* 94

* 95

* 96

* 97

* 98

* 99

* 100

* 101

* 102

* 103

* 104

* 105

* 106

* 107

* 108

* 109

* 110

* 111

* 112

* 113

* 114

* 115

* 116

![ ](/md_blog/public/assets/2021-07-25/4feda750d47e782a2976a3963e063dd0.png)  
![ ](/md_blog/public/assets/2021-07-25/0083e1bfba72d411e5dd4edf095842c7.png)

* Precautions  
--- Components of any container classLayout manager can be specified  
--- Components of the same layout manager have the same parent component  
--- The parent-child relationship is implicitly specified while setting the layout manager（`setLayout`）

![ ](/md_blog/public/assets/2021-07-25/bcc366e30a702374ca8ac034e14dfc5f.png)  
In the figure, component 1 and component 2 are managed by the same layout manager and have the same parent component.

* summary:  
--- Layout managers can be nested within each other to form a complex user interface  
--- Layout manager can be set for any container component  
--- Components in the same layout manager have the same parent component  
--- The parent-child relationship between components is an important way of memory management in Qt