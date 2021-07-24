---
layout: post
title: Qt lesson 9, dialog boxes and their types
category: qt5
tags: [qt5]
---
1\. The concept of dialog

* The dialog is with the userShort interactionofTop-level window
* QDialog is the base class of all dialog windows in Qt
* QDialog inherited from QWidget is a container type component  
![ ](/public/assets/2021-07-25/2cb10060dea54d9ece00fb78c6e3f5f4.png)
* The meaning of QDialog  
--- QDialog as aDedicated interactive windowAnd exist  
--- QDialog Can'tEmbedded in other containers as sub-components  
--- QDialog is a special QWidget with customized window style

Doubt: Since QWidget is the parent component of the QDialog window class object, why won't w.show(), the dialog box of the QDialog object pop up automatically?
    
    #include "Dialog.h" #include <QApplication> #include <QWidget> #include <QDialog> int main(int argc, char *argv[]) { QApplication a(argc, argv); QWidget w; QDialog d(&w); w.setWindowTitle("I'm QWidget"); d.setWindowTitle("I'm QDialog"); w.show(); return a.exec(); } 
    

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

![ ](/public/assets/2021-07-25/b496cfca4b4ddcf7a97a1e5e1b885ae8.png)  
Reason: Because the dialog box is an independent window, unlike buttons, these are just components. We can't think that the left and right subcomponents of QWidget are components, and there are windows. And as explained earlier, QDialog cannot be embedded in other containers as a subcomponent, so if you want to display the dialog box, you should d.show().
    
    #include "Dialog.h" #include <QApplication> #include <QWidget> #include <QDialog> int main(int argc, char *argv[]) { QApplication a(argc, argv); QWidget w; QDialog d(&w); w.show(); w.setWindowTitle("I'm QWidget"); d.show(); d.setWindowTitle("I'm QDialog"); return a.exec(); } 
    

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

![ ](/public/assets/2021-07-25/a3a5a4e3965cebbd50818c3bcc6ff212.png)  
QDialog is a top-level window, displayed on the top, and it serves as the base class of all dialog windows. The object of QWidget can also be its child components, but the final display result is
    
    #include "Dialog.h" #include <QApplication> #include <QWidget> #include <QDialog> int main(int argc, char *argv[]) { QApplication a(argc, argv); QDialog d; QWidget w(&d); w.show(); w.setWindowTitle("I'm QWidget"); d.show(); d.setWindowTitle("I'm QDialog"); return a.exec(); } 
    

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

![ ](/public/assets/2021-07-25/289ac792cbebec76c48e88904dc4256a.png)  
This is true. The parent component itself is the top-level window, and the child component is displayed in a way that we cannot see.

2\. The type of dialog box

* Modal dialog (`QDialog::exec()`）  
--- Cannot interact with the parent window after displaying  
--- is aBlockingCall dialog
* Non-modal dialog (`QDialog::show()`）  
--- After displaying, it can exist independently and can interact with the parent window at the same time  
--- is aNon-blockingDialog box call  
![ ](/public/assets/2021-07-25/bac436573b3f1cbcd47218d8f9ebb6c9.png)
* Tips  
--- Creating a modal dialog on the stack is the simplest and most common way (thanks to`QDialog::exec()`Make the window always exist)  
--- In general, non-modal dialog boxes need to be created on the heap (mainly because they are on the stack`QDialog::show()`Makes the window flash past)  
--- pass`QDialog::setModal()` The function can create a dialog with mixed characteristics, which is created on the heap like a non-modal dialog  
--- non-modal dialog needs to be specified`Qt::WA_DeleteOnClose` Attributes

Solved my long-standing doubt: My previous understanding of modal dialogs was that this window is the top-level window, and none of the next to it can be moved. But I wrote one and found that everything on my desktop can move. Suddenly I was very confused. I just understood today that the modal dialog box is a blocking dialog box. It is mainly aimed at the main window of the dialog box. That one really doesn't respond.

We generally call the first window that appears after running the main window

The operating mechanism of the mixed dialog box is a non-modal dialog box (all statements will be output), and the form of expression is a modal dialog box (the main window cannot be clicked).
    
    QDialog* dialog = new QDialog(this); dialog->setModal(this); dialog.show(); dialog.setAttribute(Qt::WA_DeleteOnClose); 
    

* 1

* 2

* 3

* 4

program:  
Dialog.h
    
    #ifndef _DIALOG_H_ #define _DIALOG_H_ #include <QDialog> #include <QPushButton> class Dialog : public QDialog { Q_OBJECT protected: QPushButton ModalBtn; QPushButton NormalBtn; QPushButton MixedBtn; protected slots: void ModalBtn_Clicked(); void NormalBtn_Clicked(); void MixedBtn_Clicked(); public: Dialog(QWidget *parent = 0); ~Dialog(); }; #endif 
    

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

Dialog.cpp
    
    #include "Dialog.h" #include <QDebug> Dialog::Dialog(QWidget *parent) :QDialog(parent), ModalBtn(this), NormalBtn(this), MixedBtn(this) { ModalBtn.setText("Modal Dialog"); ModalBtn.move(20, 20); ModalBtn.resize(100, 30); NormalBtn.setText("Normal Dialog"); NormalBtn.move(20, 70); NormalBtn.resize(100, 30); MixedBtn.setText("Mixed Dialog"); MixedBtn.move(20, 120); MixedBtn.resize(100, 30); connect(&ModalBtn, SIGNAL(clicked()), this, SLOT(ModalBtn_Clicked())); connect(&NormalBtn, SIGNAL(clicked()), this, SLOT(NormalBtn_Clicked())); connect(&MixedBtn, SIGNAL(clicked()), this, SLOT(MixedBtn_Clicked())); resize(140,170); } void Dialog::ModalBtn_Clicked() { qDebug() << "ModalBtn_Clicked() Begin"; QDialog dialog(this); dialog.resize(400,400); dialog.exec(); qDebug() << "ModalBtn_Clicked() End"; } void Dialog::NormalBtn_Clicked() { qDebug() << "NormalBtn_Clicked() Begin"; QDialog* dialog = new QDialog(this); dialog->resize(400,400); dialog->show(); dialog->setAttribute(Qt::WA_DeleteOnClose); qDebug() << "NormalBtn_Clicked() End"; } void Dialog::MixedBtn_Clicked() { qDebug() << "MixedBtn_Clicked() Begin"; QDialog* dialog = new QDialog(this); dialog->resize(400,400); dialog->setModal(this);					//Non-modal dialog box form, the nature of modal dialog box dialog->show(); dialog->setAttribute(Qt::WA_DeleteOnClose); qDebug() << "MixedBtn_Clicked() End"; } Dialog::~Dialog() { } 
    

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

main.cpp
    
    #include <QApplication> #include "Dialog.h" int main(int argc, char *argv[]) { QApplication a(argc, argv); Dialog dlg; dlg.show(); return a.exec(); } 
    

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

![ ](/public/assets/2021-07-25/fef3cf5d29e6780cd8afcd232320d7fd.png)  
3\. The return value of the dialog box

* Only modal dialogOnly the concept of return value (the user selects the dialog box to end)
* The return value of the modal dialog box is used to represent the interactive result
* `QDialog::exec()` The return value is the interactive result  
![ ](/public/assets/2021-07-25/bf39c533f8250677ef68b0a7c6b4d597.png)

Dialog.h
    
    #ifndef _DIALOG_H_ #define _DIALOG_H_ #include <QDialog> #include <QPushButton> class Dialog : public QDialog { Q_OBJECT protected: QPushButton ModalBtn; QPushButton NormalBtn; QPushButton MixedBtn; protected slots: void ModalBtn_Clicked(); void NormalBtn_Clicked(); void MixedBtn_Clicked(); public: Dialog(QWidget *parent = 0); ~Dialog(); }; #endif // DIALOG_H 
    

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

Dialog.cpp
    
    #include "Dialog.h" #include <QDebug> Dialog::Dialog(QWidget *parent) :QDialog(parent), ModalBtn(this), NormalBtn(this), MixedBtn(this) { ModalBtn.setText("Modal Dialog"); ModalBtn.move(20, 20); ModalBtn.resize(100, 30); NormalBtn.setText("Normal Dialog"); NormalBtn.move(20, 70); NormalBtn.resize(100, 30); MixedBtn.setText("Mixed Dialog"); MixedBtn.move(20, 120); MixedBtn.resize(100, 30); connect(&ModalBtn, SIGNAL(clicked()), this, SLOT(ModalBtn_Clicked())); connect(&NormalBtn, SIGNAL(clicked()), this, SLOT(NormalBtn_Clicked())); connect(&MixedBtn, SIGNAL(clicked()), this, SLOT(MixedBtn_Clicked())); resize(140,170); } void Dialog::ModalBtn_Clicked() { qDebug() << "ModalBtn_Clicked() Begin"; done(Accepted); qDebug() << "ModalBtn_Clicked() End"; } void Dialog::NormalBtn_Clicked() { qDebug() << "NormalBtn_Clicked() Begin"; done(Rejected); qDebug() << "NormalBtn_Clicked() End"; } void Dialog::MixedBtn_Clicked() { qDebug() << "MixedBtn_Clicked() Begin"; done(100); qDebug() << "MixedBtn_Clicked() End"; } Dialog::~Dialog() { qDebug() << "~Dialog()"; } 
    

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

main.cpp
    
    #include <QApplication> #include <QDebug> #include "Dialog.h" int main(int argc, char *argv[]) { QApplication a(argc, argv); Dialog dlg; int r = dlg.exec(); if(r == QDialog::Accepted) { qDebug() << "Accepted"; } else if(r == QDialog::Rejected) { qDebug() << "Rejected"; } else { qDebug() << r; } return r; } 
    

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

* summary:  
--- The dialog box is divided into modal dialog box and non-modal dialog box  
--- The modal dialog is blocking  
--- Modal dialog boxes are used in situations that rely on user interaction  
--- The non-modal dialog is non-blocking  
--- Non-modal dialog box is used for function setting occasions