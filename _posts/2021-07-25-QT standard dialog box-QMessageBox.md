---
layout: post
title: QT standard dialog box-QMessageBox
category: qt5
tags: [qt5]
---
* Record here a simple interaction method that you often encounter when interacting in development. The standard dialog box provided by qt itself, its main function, can provide users with a short message, icon and some button modal Dialog box.
In the process of using, we can roughly divide the default standard dialog box into the following categories according to the severity:
![](/md_blog/public/assets/2021-07-25/ef3feca9e0b41c22c0800f62563cfc30.JPEG)
Qt provides five types of interfaces for displaying such windows. The specific styles are as follows:
1、QMessageBox::critical(NULL, "critical", "Content", QMessageBox::Yes | QMessageBox::No, QMessageBox::Yes);
2、QMessageBox::warning(NULL, "warning", "Content", QMessageBox::Yes | QMessageBox::No, QMessageBox::Yes);
3、QMessageBox::question(NULL, "question", "Content", QMessageBox::Yes | QMessageBox::No, QMessageBox::Yes);
4、QMessageBox::about(NULL, "About", "About this application");
5\. The text information of the QMessageBox dialog box can support HTML tags. E.g:
QMessageBox::about(NULL, "About", "About this <font color='red'\>application</font\>");
6\. You can also set custom icons
Below is my routine
project files:
1. #-------------------------------------------------
2. #
3. # Project created by QtCreator 2018-01-14T15:03:03
4. #
5. #-------------------------------------------------
}QT += core gui
}greaterThan(QT_MAJOR_VERSION, 4): QT += widgets
}TARGET = inwidget
12. TEMPLATE = app
}15. SOURCES += main.cpp\
}widget.cpp
}HEADERS += widget.h
19. }#Use lamda expression to configure C++11
21. CONFIG += C++11 
}
Widget.h:
1. #ifndef WIDGET_H
2. #define WIDGET_H
3. #include <QWidget>
}7. class Widget : public QWidget
{
}Q_OBJECT
}public:
}Widget(QWidget *parent = 0);
}~Widget();
}public slots:
}void slotCriticalWidget();
}void slotWarningWidget();
}void slotQuestionWidget();
}void slotInfoWidget();
}void slotImageWidget();
}void slotDemoWidget();
}void slotDemoWidget1();
}};
}#endif // WIDGET_H
Widget.cpp:
#include "widget.h"
#include <QPushButton>
#include <QMessageBox>
}Widget::Widget(QWidget *parent)
}: QWidget(parent)
{
}QPushButton *pBtnCritical = new QPushButton(this);
}QPushButton *pBtnWarning = new QPushButton(this);
}QPushButton *pBtnQuestion = new QPushButton(this);
}QPushButton *pBtnAbout = new QPushButton(this);
}QPushButton *pBtnInformation = new QPushButton(this);
}QPushButton *PBtnImage = new QPushButton(this);
}QPushButton *pBtnQuestion1 = new QPushButton(this);
}QPushButton *pBtnDemo = new QPushButton(this);
16. }pBtnCritical->move(0,0);//Move position to position the button pBtnCritical to the coordinate (0,0)
}pBtnWarning->move(0,100);
}pBtnQuestion->move(100,0);
}pBtnAbout->move(100,100);
}pBtnInformation->move(0,50);
}PBtnImage->move(100,50);
}pBtnQuestion1->move(0, 150);
}pBtnDemo->move(100, 150);
}}pBtnCritical->setText(QString("error"));
}pBtnWarning->setText(QString("Warning"));
}pBtnQuestion->setText(QString("question"));
}pBtnAbout->setText(QString("About"));
}pBtnInformation->setText(QString("information"));
}PBtnImage->setText(QString("Custom"));
}pBtnQuestion1->setText(QString("Question"));
}pBtnDemo->setText(QString("Question 1"));
}37. }connect(pBtnCritical, &QPushButton::clicked, this, &Widget::slotCriticalWidget);//The signal and slot mechanism in Qt5
}connect(pBtnWarning, SIGNAL(clicked()), this, SLOT(slotWarningWidget()));//The signal and slot mechanism in QT4, QT4 does not do parameter matching correction, even if there is no slot function, the compilation will be able to pass 
}connect(pBtnQuestion, &QPushButton::clicked, this, &Widget::slotQuestionWidget);
}connect(pBtnInformation, &QPushButton::clicked, this, &Widget::slotInfoWidget);
}connect(PBtnImage, &QPushButton::clicked, this, &Widget::slotImageWidget);
}connect(pBtnQuestion1, &QPushButton::clicked, this, &Widget::slotDemoWidget);
}connect(pBtnDemo, &QPushButton::clicked, this, &Widget::slotDemoWidget1);
}//Lamda expression
}connect(pBtnAbout, &QPushButton::clicked,
}[=]()
}{
}QMessageBox::about(NULL, QString(tr("About")), QString(tr("This is the About dialog box")));
}}
});
}}
}Widget::~Widget()
{
58. }
}void Widget::slotCriticalWidget()
{
}QMessageBox *pMegBox = new QMessageBox(QString(tr("error")), QString(tr("this is an error message box!")),
}QMessageBox::Critical,//Here is the icon displayed in the message box
}QMessageBox::Ok | QMessageBox::Default,// Here is the button on the message box, the cursor is positioned by default
}QMessageBox::Cancel | QMessageBox::Escape, //This is combined with the escape key on the keyboard. When the user presses the key. The message box will execute the cancel key event
}0);// Define the third button here
68. // pMegBox->setAttribute(Qt::WA_DeleteOnClose, true);
}pMegBox->show();
70. }
}void Widget::slotWarningWidget()
{
}QMessageBox::warning(this, QString(tr("Warning")), QString(tr("This is a warning dialog")), QMessageBox::Yes|QMessageBox::No);//Set the parent object to this, delete the object when the software is closed
}
}void Widget::slotQuestionWidget()
{
}switch(QMessageBox::question(this, QString(tr("question")), QString(tr("What is your gender?")), QString(tr("Male")), QString(tr(" " )), QString(tr(" ")), 0, 1))
}{
}case 0:
}break;
}case 1:
}break;
}case 2:
}break;
}default:
}break;
}}
91. }
}void Widget::slotInfoWidget()
{
}QMessageBox* pMeg = new QMessageBox();
}pMeg->setInformativeText(QString(" <font color='red'>Hello</font>, welcome"));
}pMeg->setAttribute(Qt::WA_DeleteOnClose,true);
}pMeg->show();
}
}void Widget::slotImageWidget()
{
}QMessageBox message(QMessageBox::NoIcon, "Title", QString(tr("custom icon")));
}message.setIconPixmap(QPixmap("13.png"));
}message.exec();
}
}void Widget::slotDemoWidget()
{
}auto ret = QMessageBox::question(this, QString("question"), QString("Can you give me a hundred yuan?"),
}QMessageBox::Yes | QMessageBox::No | QMessageBox::Save,
}QMessageBox::No);
114. }switch (ret) {
}case QMessageBox::Yes:
}break;
}case QMessageBox::No:
}break;
}case QMessageBox::Save:
}break;
}default:
}break;
}}
}
}128. void Widget::slotDemoWidget1()
{
}QMessageBox msg(QMessageBox::Information, QString("Question"), QString("Do you want to be a great god?"));
}msg.setInformativeText(QString("Don't hesitate if you think!"));
}msg.setDetailedText(QString("Get started!"));//Adding detailed information will automatically add a button
133. }msg.setStandardButtons(QMessageBox::Ok | QMessageBox::Discard | QMessageBox::Cancel);
}msg.setDefaultButton(QMessageBox::Ok);//Set the default button
136. }QPushButton *Okbtn = new QPushButton(QObject::tr("wash and sleep"));
}msg.addButton(Okbtn, QMessageBox::AcceptRole);//Add custom buttons
139. }auto ret = msg.exec();
}switch (ret) {
}case QMessageBox::Ok:
}break;
144. }case QMessageBox::Discard:
}break;
147. }case QMessageBox::Cancel:
}break;
150. }case QMessageBox::AcceptRole:
}break;
}default:
}break;
}}
}
}}}}165. 
main.cpp:
#include "widget.h"
#include <QApplication>
}int main(int argc, char *argv[])
{
}QApplication a(argc, argv);
}Widget w;
}w.show();
9. }return a.exec();
}
![](/md_blog/public/assets/2021-07-25/498f9e6bda38f2c9c5ccca1f5a3a9464.png)
![](/md_blog/public/assets/2021-07-25/e157c9a0a9e54e80fdd56cc76ce61282.png)
![](/md_blog/public/assets/2021-07-25/a1d5ded8f083bf0ddabe5be3312ed5a6.png) ![](/md_blog/public/assets/2021-07-25/394e8f1f9a0b6d6787df89a7b10ebbaf.png)
![](/md_blog/public/assets/2021-07-25/e4f3e6c4319cc552bb2df3dacb4002cd.png) ![](/md_blog/public/assets/2021-07-25/dc448e3b6ebc0ad006b7196392116989.png)