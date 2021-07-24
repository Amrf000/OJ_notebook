---
layout: post
title: Use of QT5 mac QtXlsxWriter
category: qt5
tags: [qt5]
---
I studied QtXlsxWriter's reading and writing of xlsx, and shared the process of writing here:
    
    git clone https://github.com/VSRonin/QtXlsxWriter.git


1. cd QtXlsxWriter
    

2. qmake
    

3. make -j8
    

4. sudo make install
    
    

Then the installation was successful.

Then open Qtcreated and create a QT project. Plus:
    
    QT += xlsx

Then in my mainwindows.cpp the following:
    

1. #include "mainwindow.h"
    

2. #include "ui_mainwindow.h"
    

3. #include <QMessageBox>
    

4. #include <QtXlsx>
    

5. 6. MainWindow::MainWindow(QWidget *parent) :
    

7.  QMainWindow(parent),
    

8.  ui(new Ui::MainWindow)
    

9. {
    

10.  ui->setupUi(this);
    

11.  QXlsx::Document xlsx;
    

12.  xlsx.write("A1", "Hello Qt!");
    

13.  xlsx.saveAs("/Users/eric/Documents/qt_projects/Test.xlsx");
    

14. 15. 16. }
    

17. 18. MainWindow::~MainWindow()
    

19. {
    

20.  delete ui;
    

21. }
    
    

When the operation is completed, you will find that there is one more Test.xlsx in the qt\_projects directory. If you want to know more functions, please refer to the following documents.

# references

\[1\]. VSRonin/QtXlsxWriter. [https://github.com/VSRonin/QtXlsxWriter](https://github.com/VSRonin/QtXlsxWriter)

\[2\]. Qt Xlsx. [http://qtxlsx.debao.me/](http://qtxlsx.debao.me/)