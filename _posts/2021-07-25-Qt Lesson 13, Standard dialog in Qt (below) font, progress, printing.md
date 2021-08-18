---
layout: post
title: Qt Lesson 13, Standard dialog in Qt (below) font, progress, printing
category: qt5
tags: [qt5]
---
1\. Font dialog
* Qt provides a predefined font dialog`QFontDialog` class
* `QFontDialog`Classes are used to provide dialog components for selecting fonts  
![ ](/md_blog/public/assets/2021-07-25/63bf4e94bc5a18b0fdcdae0e1b64aee0.png)
* How to use the font dialog  
![ ](/md_blog/public/assets/2021-07-25/ad18a28c40d91ea988af9a69e1d19106.png)
program:
Widget.h
    #ifndef WIDGET_H #define WIDGET_H #include <QWidget> #include <QPushButton> #include <QDebug> class Widget : public QWidget { Q_OBJECT private: QPushButton FontBtn; QPushButton ProgressBtn; QPushButton PrintBtn; private slots: void FontBtn_Clicked(); void ProgressBtn_Clicked(); void PrintBtn_Clicked(); public: explicit Widget(QWidget *parent = 0); signals: public slots: }; #endif 
Widget.cpp
    #include "Widget.h" #include <QFontDialog> #include <QProgressDialog> #include <QtPrintSupport/QPrintDialog> Widget::Widget(QWidget *parent) : QWidget(parent), FontBtn(this),ProgressBtn(this),PrintBtn(this) { FontBtn.setText("Font Dialog"); FontBtn.move(20,20); FontBtn.resize(140,30); ProgressBtn.setText("Progress Dialog"); ProgressBtn.move(20,70); ProgressBtn.resize(140,30); PrintBtn.setText("Print Dialog"); PrintBtn.move(20,120); PrintBtn.resize(140,30); setFixedSize(180,170); connect(&FontBtn,SIGNAL(clicked()),this,SLOT(FontBtn_Clicked())); connect(&ProgressBtn,SIGNAL(clicked()),this,SLOT(ProgressBtn_Clicked())); connect(&PrintBtn,SIGNAL(clicked()),this,SLOT(PrintBtn_Clicked())); } void Widget::FontBtn_Clicked() { QFontDialog dlg(this); dlg.setWindowTitle("Font Dialog Test"); dlg.setCurrentFont(QFont("Courier New",10,QFont::Bold)); if(dlg.exec() == QFontDialog::Accepted) { qDebug() << dlg.selectedFont(); } } void Widget::ProgressBtn_Clicked() { } void Widget::PrintBtn_Clicked() { } 
main.cpp
    #include "Widget.h" #include <QApplication> int main(int argc, char *argv[]) { QApplication a(argc, argv); Widget w; w.show(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/81671fa20e8f6967cc1cf35dba9bd510.png)  
![ ](/md_blog/public/assets/2021-07-25/c43fe33779d52e1e2fe980b31de52eac.png)
* `QFontDialog` Utility functions in  
--- `QFontDialog::getFont`
     bool ok; QFont font = QFontDialog::getFont(&ok, QFont("Courier New",10,QFont::Bold), this); if (ok) { // font is set to the font the user selected } else { // the user canceled the dialog; font is set to the initial // value, in this case Times, } 
2\. Progress dialog
* Qt provides a predefined progress dialog`QPropressDialog` class
* `QPropressDialog`Class is used to display progress information
* `QPropressDialog`Classes are used when users need to wait  
![ ](/md_blog/public/assets/2021-07-25/e5cf2973c8b73752752ad5e13b8c68b6.png)
* How to use the progress dialog  
![ ](/md_blog/public/assets/2021-07-25/dd1acc363664916c4f5d928307720596.png)
     void Widget::ProgressBtn_Clicked() { QProgressDialog dlg(this); dlg.setWindowTitle("Updating from server..."); dlg.setLabelText("Download from server ..."); dlg.setMinimum(0); dlg.setMaximum(100); dlg.setValue(35); //creat a new thread; dlg.exec(); } 
3\. Print dialog
* Qt provides a predefined print dialog`QPrintDialog` class
* `QPrintDialog` Class is used to set printing related parameter information  
![ ](/md_blog/public/assets/2021-07-25/c05703594ad788aaca564f78fde4a866.png)
Knowledge points:
* In Qt`QPrinter` Class is the packaging of printing equipment and its parameters
* `QPrinter` Class encapsulates the drive interface of the printing device in the system
* `QPrinter` In the same wayUse different printing devices in the system
    void Widget::PrintBtn_Clicked() { QPrintDialog dlg(this); dlg.setWindowTitle("Print Dialog"); if(dlg.exec() == QPrintDialog::Accepted) { QPrinter* p = dlg.printer(); //Indicates a printer object QTextDocument td; //Indicates text document // td.setPlainText("Printer Object test"); td.setHtml("<h1>Print html object test</h1>"); p->setOutputFileName("E:\\test.xps"); td.print(p); } } 
summary
* Qt standard dialog design mode  
--- GUI interface generates data objects  
--- Other objects in the business logic use data objects  
--- GUI interface and business logic are connected through data objects  
![ ](/md_blog/public/assets/2021-07-25/4d0f1d6f7c83c6efd487cc1188732358.png)
