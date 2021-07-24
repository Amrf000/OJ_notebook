---
layout: post
title: Lesson 26, Comprehensive Example of Layout Manager
category: qt5
tags: [qt5]
---






# 1\. Demand analysis

1\. Practice developing a wizard user interface

(1) Display different wizard pages on the same interface

(2) Switch through the "Previous" and "Next" buttons

(3) The element components and element arrangement on different pages are different

(4) The components in the page are arranged through the layout manager

# Two, the solution

1\. Interface design through layout nesting

![](/md_blog/public/assets/2021-07-25/9bc0d25cc01402efe5556dedb14ba9ac.png)

2\. Manage different pages through QStackedLayout

![](/md_blog/public/assets/2021-07-25/0edcc7dae56d9257655ab3b88182ebac.png)

3\. Generate different ways through sub-components

![](/md_blog/public/assets/2021-07-25/5cc8f14905c961c8785edc241eb5d86e.png)

4\. Matters needing attention

(1) Layout manager can be specified for any container component

(2) Components in the same layout manager have the same parent component

(3) The parent-child relationship is implicitly specified while the layout management is set

![](/md_blog/public/assets/2021-07-25/1ed2bdd812507951af1ec7bd9dc1da31.png)

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) Widget.h


1. #ifndef WIDGET_H


2. #define WIDGET_H


3. #include <QtGui/QWidget>


#include <QLabel>


#include <QLineEdit>


#include <QPushButton>


#include <QStackedLayout>


}class Widget : public QWidget


{


}Q_OBJECT


13. private:


}QLabel label1;


}QLabel label2;


}QLabel label3;


}QLabel label4;


}QLineEdit edit;


}QPushButton pageBtn1;


}QPushButton pageBtn2;


21. }QStackedLayout sLayout;//The definition is here for the convenience of the slot function


23. }void initControl();


}QWidget* pageone();


}QWidget* pagetwo();


}QWidget* pagethree();


}private slots:


}void onPreBtnClicked();


}void onNextBtnClicked();


32. public:


}Widget(QWidget *parent = 0);


}~Widget();


};


}#endif // WIDGET_H


}Widget.h



![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) Widget.cpp


#include "Widget.h"


#include <QHBoxLayout>


#include <QVBoxLayout>


#include <QPushButton>


#include <QFormLayout>


#include <QGridLayout>


#include <QDebug>


}Widget::Widget(QWidget *parent)


}: QWidget(parent)


{


}initControl();


}


14. void Widget::initControl()


{


}QHBoxLayout* hLayout = new QHBoxLayout();//1. Define the horizontal, vertical and stack manager of the main interface


}QVBoxLayout* vLayout = new QVBoxLayout();


}}QPushButton* preBtn = new QPushButton();


}QPushButton* nextBtn = new QPushButton();


}preBtn->setText("pre page");


}nextBtn->setText("next page");


}preBtn->setMinimumSize(100,30);


}nextBtn->setMinimumSize(100,30);


26. }hLayout->addWidget(preBtn);//3. Define the button and add it to the level manager


}hLayout->addWidget(nextBtn);


29. }sLayout.addWidget(pageone());//5. Implement the page and add it to the stack manager


}sLayout.addWidget(pagetwo());


}sLayout.addWidget(pagethree());


33. }vLayout->addLayout(&sLayout);//2. Add horizontal and stack manager to vertical manager


}vLayout->addLayout(hLayout);


}setLayout(vLayout);


37. }connect(preBtn, SIGNAL(clicked()), this, SLOT(onPreBtnClicked()));//6.Connect signal and slot


}connect(nextBtn, SIGNAL(clicked()), this, SLOT(onNextBtnClicked()));


}}


}QWidget* Widget::pageone()


{


}QWidget* ret = new QWidget;


}QGridLayout* glayout = new QGridLayout();


48. }label1.setText("one");


}label2.setText("two");


}label3.setText("three");


}label4.setText("four");


}glayout->addWidget(&label1, 0, 0);


}glayout->addWidget(&label2, 0, 1);


}glayout->addWidget(&label3, 1, 0);


}glayout->addWidget(&label4, 1, 1);


57. }ret->setLayout(glayout);


}/*Indicates that the components in the same layout manager have the same parent component


}qDebug() << ret;


}qDebug() << label1.parent();


}qDebug() << label2.parent();


}qDebug() << label3.parent();


}qDebug() << label4.parent();


65. */


}return ret;


}


68. QWidget* Widget::pagetwo()


{


}QWidget* ret = new QWidget;


}QFormLayout* flayout = new QFormLayout();


72. }flayout->addRow("name:", &edit);


}ret->setLayout(flayout);


75. }return ret;


}


78. QWidget* Widget::pagethree()


{


}QWidget* ret = new QWidget;


81. }pageBtn1.setText("this is");


}pageBtn2.setText("a page");


84. }QVBoxLayout* vlayout = new QVBoxLayout();


}vlayout->addWidget(&pageBtn1);


}vlayout->addWidget(&pageBtn2);


88. }ret->setLayout(vlayout);


90. }return ret;


}


93. void Widget::onPreBtnClicked()


{


}int index = ((sLayout.currentIndex() - 1) + sLayout.count()) % sLayout.count();


}sLayout.setCurrentIndex(index);


}


98. void Widget::onNextBtnClicked()


{


}int index = (sLayout.currentIndex() + 1) % 3;


}sLayout.setCurrentIndex(index);


}


103. Widget::~Widget()


{


105. }


107. Widget.cpp



![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) main.cpp


#include <QtGui/QApplication>


#include "Widget.h"


}int main(int argc, char *argv[])


{


}QApplication a(argc, argv);


}Widget w;


}w.show();


9. }return a.exec();


}


12. main.cpp



# 2\. Summary

(1) The layout manager can be nested to form a complex user interface

(2) Layout manager can be set for any container component

(3) The components in the same layout manager have the same parent component

(4) The parent-child relationship between components is an important way of memory management in Qt