---
layout: post
title: Qt Lesson 8-Calculator Interface Design
category: qt5
tags: [qt5]
---
This article is learned from the QT course of Tang Zuolin from Ditai Software. The pictures in the article are from the teacher's course PPT.

---

Experiment 1: Calculator interface

![ ](/public/assets/2021-07-25/6d34c6530497eb0a61b4036318c30e70.png)  
![ ](/public/assets/2021-07-25/a7a16b634b809f4ce271500a2e42a35d.png)  
![ ](/public/assets/2021-07-25/a04d12bce9ca3d3614024501c341e8de.png)  
![ ](/public/assets/2021-07-25/81e20f8e61ad4538209acae089c1732e.png)  
Issues to note:  
![ ](/public/assets/2021-07-25/be6c98ebcca30220095a1369edbfdcf9.png)

Checking documents while developing

Experiment: Calculator interface
    
    #include <QtGui/QApplication> #include <QWidget> //Main window #include <QLineEdit> //Text box #include <QPushButton> //Button int main(int argc, char *argv[]) { QApplication a(argc, argv); QWidget* w = new QWidget(NULL, Qt::WindowCloseButtonHint);//Remove the window maximize and minimize buttons QLineEdit* le = new QLineEdit(w); QPushButton* button[20] = {0};//Object pointer array //Button string array const char* btnText[20] = { "7", "8", "9", "+", "(", "4", "5", "6", "-", ")", "1", "2", "3", "*", "<-", "0", ".", "=", "/", "C", }; int ret = 0; //Text box coordinates, size le->move(10, 10); le->resize(240, 30); le->setReadOnly(true);//The text box does not accept the user's direct input of characters // Treat the button interface as a two-dimensional array. Four rows and five columns for(int i=0; i<4; i++) { for(int j=0; j<5; j++) { button[i*5 + j] = new QPushButton(w); button[i*5 + j]->resize(40, 40); button[i*5 + j]->move(10 + (10 + 40)*j, 50 + (10 + 40)*i); button[i*5 + j]->setText(btnText[i*5 + j]);//button string } } w->show(); w->setFixedSize(w->width(), w->height());//Fix the size of the window, you cannot pull the window size ret = a.exec(); delete w; return ret; } 
    

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

![ ](/public/assets/2021-07-25/4f6e3547f54816795e3759d31385efeb.png)  
![ ](/public/assets/2021-07-25/077f1bab1ee8ed1d2fffee8a3238677b.png)