---
layout: post
title: Lesson 54 Multi-page switching component in Qt
category: qt5
tags: [qt5]
---
4.3M
Ubuntu 18.04 Preview of New Features
![ ](/md_blog/public/assets/2021-07-25/7dc22a6cea53bdba4b24ec2622bc8e34.png)  
![ ](/md_blog/public/assets/2021-07-25/7563ae71352aca875fa8b6bfe92471f6.png)  
![ ](/md_blog/public/assets/2021-07-25/c3b5983e544e781f6dcaff5ed4926a92.png)  
![ ](/md_blog/public/assets/2021-07-25/3b06f7015ec1242d09e8c9b8b3b01365.png)  
![ ](/md_blog/public/assets/2021-07-25/55d835a2f72685caed9e1c9bcf2d3cb0.png)  
Widget.h
```
#ifndef WIDGET_H
#define WIDGET_H
#include <QTabWidget>
#include <QWidget>
class Widget : public QWidget {
  Q_OBJECT private : QTabWidget m_tabwidget;

public:
  Widget(QWidget *parent = nullptr);
  ~Widget();
};
#endif // WIDGET_H
```
Widget.cpp
```
#include "Widget.h"
#include <QLabel>
#include <QPlainTextEdit>
#include <QPushButton>
#include <QVBoxLayout>
Widget::Widget(QWidget *parent) : QWidget(parent) {
  m_tabwidget.setParent(this);
  m_tabwidget.move(10, 10);
  m_tabwidget.resize(200, 200);
  QPlainTextEdit *edit = new QPlainTextEdit(&m_tabwidget);
  edit->insertPlainText("xiebs");
  m_tabwidget.addTab(edit, "1st");
  QWidget *widget = new QWidget(&m_tabwidget);
  QVBoxLayout *layout = new QVBoxLayout(&m_tabwidget);
  QLabel *label = new QLabel(&m_tabwidget);
  label->setText("2nd Tab Page");
  label->setAlignment(Qt::AlignCenter);
  QPushButton *btn = new QPushButton(&m_tabwidget);
  btn->setText("2nd Tab Page");
  layout->addWidget(label);
  layout->addWidget(btn);
  widget->setLayout(layout);
  m_tabwidget.addTab(widget, "2st");
}
Widget::~Widget() {}
```
main.cpp
```
#include "Widget.h"
#include <QApplication>
int main(int argc, char *argv[]) {
  QApplication a(argc, argv);
  Widget w;
  w.show();
  return a.exec();
}
```
![ ](/md_blog/public/assets/2021-07-25/f0a3cd3e7f0753ee5c8340f76332ba6b.png)
![ ](/md_blog/public/assets/2021-07-25/e9d1cefad62a2f695a83982b2df3816d.png)  
![ ](/md_blog/public/assets/2021-07-25/5cd5ec54ea6e248bef5bfb44a089ebbf.png)
![ ](/md_blog/public/assets/2021-07-25/d7fee536cff24124c0ae2df185f9c614.png)  
Widget.h
```
#ifndef WIDGET_H
#define WIDGET_H
#include <QTabWidget>
#include <QWidget>
class Widget : public QWidget {
  Q_OBJECT protected : QTabWidget m_tabwidget;
protected slots:
  void onCurrentChanged(int index);
  void onTabCloseRequested(int index);

public:
  Widget(QWidget *parent = nullptr);
  ~Widget();
};
#endif // WIDGET_H
```
Widget.cpp
```
#include "Widget.h"
#include <QDebug>
#include <QLabel>
#include <QPlainTextEdit>
#include <QPushButton>
#include <QResizeEvent>
#include <QSizePolicy>
#include <QVBoxLayout>
Widget::Widget(QWidget *parent) : QWidget(parent) {
  QVBoxLayout *m_layout = new QVBoxLayout;
  m_tabwidget.setParent(this);
  m_tabwidget.move(
      10,
      10); // m_tabwidget.resize(200, 200);
           // m_tabwidget.setTabPosition(QTabWidget::South);
           // m_tabwidget.setTabShape(QTabWidget::Triangular);
           // m_tabwidget.setTabsClosable(true); QPlainTextEdit* edit = new
           // QPlainTextEdit(&m_tabwidget); edit->insertPlainText("xiebs");
           // m_tabwidget.addTab(edit, "1st"); QWidget* widget = new
           // QWidget(&m_tabwidget); QVBoxLayout* layout = new
           // QVBoxLayout(&m_tabwidget); QLabel* label = new
           // QLabel(&m_tabwidget); label->setText("2nd Tab Page");
           // label->setAlignment(Qt::AlignCenter); QPushButton* btn = new
           // QPushButton(&m_tabwidget); btn->setText("2nd Tab Page");
           // layout->addWidget(label); layout->addWidget(btn);
           // widget->setLayout(layout); m_tabwidget.addTab(widget, "2st");
           // m_tabwidget.addTab(&m_edit, "3st");
           // m_layout->addWidget(&m_tabwidget); setLayout(m_layout);
           // connect(&m_tabwidget, SIGNAL(currentChanged(int)), this,
           // SLOT(onCurrentChanged(int))); connect(&m_tabwidget,
           // SIGNAL(tabCloseRequested(int)), this,
           // SLOT(onTabCloseRequested(int))); } void
           // Widget::onCurrentChanged(int index) { qDebug() << "Page index:"
           // << index; } void Widget::onTabCloseRequested(int index) {
           // m_tabwidget.removeTab(index); } Widget::~Widget() { }
```
summary
* The Qt platform provides powerful multi-page components
* QTabWidget component can only add one component at a time
* When multiple components are added, it is done through container components and layout managers
* QTabWidget can customize the appearance and position of page tabs
* The predefined signals of QTabWidget can realize advanced functions in the program
