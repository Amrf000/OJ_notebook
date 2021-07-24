---
layout: post
title: Qt standard dialog box QFONTDIALOG
category: qt5
tags: [qt5]
---
* // Here is a brief introduction
    public slots: void FontDlg(); private: QLineEdit *line;
//Constructor
    MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent) { resize(600,600); QPushButton *btn = new QPushButton(tr(Modify font),this); btn->move(200,200); line = new QLineEdit(this); line->move(200,150); connect(btn,&QPushButton::clicked,this,&MainWindow::FontDlg); }
FontDlg
    void MainWindow::FontDlg() { bool ok; QFont font = QFontDialog::getFont(&ok,this); if(ok) line->setFont(font); }