---
layout: post
title: QT Foundation (3) Dialog QD
category: qt5
tags: [qt5]
---
# 

## 

The content of this article:  
1\. Distinguish and use modal and non-modal dialogs.  
2\. Multi-window switching.

Modal and non-modal dialogs.
> 
> Modal dialog: When it pops up, other windows of the application will no longer accept user input. Only the dialog responds to user input, and other windows can continue to interact with the user after exiting it. (For example: "Save as" in word)  
> Modeless dialog: After it pops up, other windows of the program can still respond to user input. Non-modal dialogs are generally used to display prompts and so on. (For example: "find and replace" in word

Modeless dialog  
Create the Qt Widgets application project, select the QWidget for the base class, name the class name mywidget, and add the code to the mywidget.cpp file:
    
    #include "mywidget.h" #include "ui_mywidget.h" #include<QDialog> MyWidget::MyWidget(QWidget *parent) : QWidget(parent), //Define a QDialog class object in the constructor of the MyWidget class. ui(new Ui::MyWidget) { ui->setupUi(this); QDialog *dialog = new QDialog (this); / / with new equivalent to open up a new memory space, this role specifies the parent window of the dialog for the MyWidget class object dialog->show(); } MyWidget::~MyWidget() { delete ui; } 
    

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

Code interpretation:QDialog \*dialog defines a pointer to a QDialog class object (also a way to create an object, but requires new to open up new memory space) instead of defining a new object. Here the dialog specifies the parent window, so there is no need to release the object.
> 
> -\> is an operator of the C and C++ languages, called the structure member operator, which uses a pointer to a structure or object to access its members.  
> Thinking: Deep Thinking -\> Show Usage Differences in .show

operation result:  
mydialog1 is the dialog and mywidget is the window.  
![ ](/public/assets/2021-07-25/0f23110f2607feb3011a5fb0b2e4402d.png)  
Create a modal dialog with .exec() without pointers
    
    QDialog dialog（this）； dialog.exec(); 
    

* 1

* 2

operation result: The mydialog1 dialog box pops up and the mywidget window appears after the dialog box is closed. This dialog is a modal dialog.

Create a modal dialog with the show() function
    
     QDialog *dialog =new QDialog(this); dialog->setModal(true); dialog->show(); 
    

* 1

* 2

* 3

operation result: Same as the first result, but you can only close the mydialog1 dialog before closing the mywidget window.
> 
> Summary: To make a dialog box a modal dialog, use the .exec() function call; to be a modeless dialog, create it with new and call it with the .show() function.
> 
> The difference between .show() and .exec() is that control is passed to the caller after the show is called, and the program continues to proceed, and exec can only be returned when the dialog is closed.  
> Thinking: The role of the setModal function.