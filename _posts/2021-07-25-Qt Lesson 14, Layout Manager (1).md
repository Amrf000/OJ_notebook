---
layout: post
title: Qt Lesson 14, Layout Manager (1)
category: qt5
tags: [qt5]
---
# 

## 

##### 

### 

Existing problems

* Current GUI development method: absolute positioning
* Problem: The position and size of the component cannot adapt to changes in the window

1\. Layout Manager(Layout: layout)

--- Ability to automatically arrange interface components in windows  
--- automatically update the size of the interface components after the window changes

* `QLayout` Is an abstract base class for layout managers in Qt
* Through inheritance`QLayout` Implement different and complementary layout managers
* Qt can customize the layout manager as needed
* Layout managerNot an interface component, But the positioning strategy of the interface components (not visible in the interface, is the helper of the window)  
![ ](/public/assets/2021-07-25/2a2db3e3303888441c1297dd8b0344bc.png)  
2\. Introduction
* `QBoxLayout` Layout manager  
--- toHorizontal or verticalWay to manage interface components  
![ ](/public/assets/2021-07-25/7375372311a5dfa027346ed387c9e431.png)  
![ ](/public/assets/2021-07-25/8fd45efa72ae9f060bdf4bfd8004f56b.png)
    
    QVBoxLayout: the length is changing, the height is not changing 
    

* 1

Widget.h
    
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> class Widget : public QWidget { Q_OBJECT protected: QPushButton Btn1; QPushButton Btn2; QPushButton Btn3; QPushButton Btn4; void init(); void testVBoxLayout(); void testHBoxLayout(); void testVHBoxLayout(); public: Widget(QWidget *parent = nullptr); ~Widget(); }; #endif 
    

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

Widget.cpp
    
    #include "Widget.h" #include <QLayout> #include <QBoxLayout> #include <QVBoxLayout> #include <QHBoxLayout> Widget::Widget(QWidget *parent): QWidget(parent), Btn1(this), Btn2(this), Btn3(this), Btn4(this) { //init(); //testVBoxLayout(); //testHBoxLayout(); testVHBoxLayout(); } void Widget::init() { Btn1.setText("Test Button 1"); Btn1.move(20,20); Btn1.resize(140,30); Btn2.setText("Test Button 2"); Btn2.move(20,70); Btn2.resize(140,30); Btn3.setText("Test Button 3"); Btn3.move(20,120); Btn3.resize(140,30); Btn4.setText("Test Button 4"); Btn4.move(20,170); Btn4.resize(140,30); } void Widget::testVBoxLayout() { //The steps here are in the help documentation QVBoxLayout* layout = new QVBoxLayout(); //Set to vertical layout Btn1.setText("Test Button 1"); Btn1.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); //Set the size to change with the window Btn1.setMinimumSize(140, 30); //Set the minimum size of the button Btn2.setText("Test Button 2"); Btn2.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn2.setMinimumSize(140, 30); Btn3.setText("Test Button 3"); Btn3.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn3.setMinimumSize(140, 30); Btn4.setText("Test Button 4"); Btn4.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn4.setMinimumSize(140, 30); layout->setSpacing(30); //Set the minimum gap between buttons layout->addWidget(&Btn1); layout->addWidget(&Btn2); layout->addWidget(&Btn3); layout->addWidget(&Btn4); setLayout(layout); //Set layout management } void Widget::testHBoxLayout() { //The steps here are in the help documentation QHBoxLayout* layout = new QHBoxLayout(); //Set to vertical layout Btn1.setText("Test Button 1"); Btn1.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); //Set the size to change with the window Btn1.setMinimumSize(140, 30); //Set the minimum size of the button Btn2.setText("Test Button 2"); Btn2.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn2.setMinimumSize(140, 30); Btn3.setText("Test Button 3"); Btn3.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn3.setMinimumSize(140, 30); Btn4.setText("Test Button 4"); Btn4.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn4.setMinimumSize(140, 30); layout->setSpacing(30); //Set the minimum gap between buttons layout->addWidget(&Btn1); layout->addWidget(&Btn2); layout->addWidget(&Btn3); layout->addWidget(&Btn4); setLayout(layout); } void Widget::testVHBoxLayout() { QVBoxLayout* vlayout1 = new QVBoxLayout(); QVBoxLayout* vlayout2 = new QVBoxLayout(); QHBoxLayout* hlayout3 = new QHBoxLayout(); Btn1.setText("Test Button 1"); Btn1.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); //Set the size to change with the window Btn1.setMinimumSize(140, 30); //Set the minimum size of the button Btn2.setText("Test Button 2"); Btn2.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn2.setMinimumSize(140, 30); vlayout1->setSpacing(30); vlayout1->addWidget(&Btn1); vlayout1->addWidget(&Btn2); Btn3.setText("Test Button 3"); Btn3.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn3.setMinimumSize(140, 30); Btn4.setText("Test Button 4"); Btn4.setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding); Btn4.setMinimumSize(140, 30); vlayout2->setSpacing(30); vlayout2->addWidget(&Btn3); vlayout2->addWidget(&Btn4); hlayout3->setSpacing(30); hlayout3->addLayout(vlayout1); hlayout3->addLayout(vlayout2); setLayout(hlayout3); } Widget::~Widget() { } 
    

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

* 117

* 118

* 119

* 120

* 121

* 122

* 123

* 124

* 125

* 126

* 127

* 128

* 129

* 130

* 131

* 132

* 133

* 134

* 135

* 136

* Layout managers can be nested with each other to form a more complex layout  
--- Layout nesting can complete almost all commonly used interface layouts  
--- Custom layout class can achieve the effect of personalized interface  
![ ](/public/assets/2021-07-25/0b5baee9a6d7739f1e30d06e1085631a.png)
* summary  
--- Absolutely positioned layout cannot adapt to changes in the window  
--- Qt provides related classes for layout management of interface components  
--- Qt is predefinedDifferent functions and complementaryLayout manager  
--- The layout manager canNesting each other to form a complex layout