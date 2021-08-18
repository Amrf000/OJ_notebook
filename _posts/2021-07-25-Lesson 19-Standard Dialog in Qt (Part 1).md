---
layout: post
title: Lesson 19-Standard Dialog in Qt (Part 1)
category: qt5
tags: [qt5]
---
![](/md_blog/public/assets/2021-07-25/24becc4d41299cba9aff655dddb00933.png)
![](/md_blog/public/assets/2021-07-25/b53b3dc0e363b8bdbb2d009eb35df880.png)
![](/md_blog/public/assets/2021-07-25/745c059a53568da5aff2117fbbff6060.png)
![](/md_blog/public/assets/2021-07-25/b66ea59c2dbff83641fb89463aeb2bb9.png)
![](/md_blog/public/assets/2021-07-25/2cc185efc9483fc417935042bb977909.png)
![](/md_blog/public/assets/2021-07-25/5a73b1da7fde824b7318fd3576ef2050.png)
![](/md_blog/public/assets/2021-07-25/02922b32d8f8f516feb42e30c86487d2.png)
![](/md_blog/public/assets/2021-07-25/a4ab73c91ae390229e5c056827f57b9c.png)
![](/md_blog/public/assets/2021-07-25/8c3e75b1a0fe68df302b4f7b5d2a49c6.png)
![](/md_blog/public/assets/2021-07-25/916ffe5939f05670874ee50dfb9ad569.png)
![](/md_blog/public/assets/2021-07-25/c763efe2f7438c24df8bb01dad4afaa5.png)
#include <QtGui/QApplication>
#include "Widget.h"
}int main(int argc, char *argv[])
{
}QApplication a(argc, argv);
}Widget w;
8. }w.show();
10. }return a.exec();
}
#include "Widget.h"
#include <QDebug>
#include <QMessageBox>
#include <QFileDialog>
}7. Widget::Widget(QWidget *parent) : QWidget(parent),
}SimpleMsgBtn(this), CustomMsgBtn(this), OpenFileBtn(this), SaveFileBtn(this)
{
}SimpleMsgBtn.setText("Simple Message Dialog");
}SimpleMsgBtn.move(20, 20);
}SimpleMsgBtn.resize(160, 30);
13. }CustomMsgBtn.setText("Custom Message Dialog");
}CustomMsgBtn.move(20, 70);
}CustomMsgBtn.resize(160, 30);
17. }OpenFileBtn.setText("Open File Dialog");
}OpenFileBtn.move(20, 120);
}OpenFileBtn.resize(160, 30);
21. }SaveFileBtn.setText("Save File Dialog");
}SaveFileBtn.move(20, 170);
}SaveFileBtn.resize(160, 30);
25. }resize(200, 220);
}setFixedSize(200, 220);
28. }connect(&SimpleMsgBtn, SIGNAL(clicked()), this, SLOT(SimpleMsgBtn_Clicked()));
}connect(&CustomMsgBtn, SIGNAL(clicked()), this, SLOT(CustomMsgBtn_Clicked()));
}connect(&OpenFileBtn, SIGNAL(clicked()), this, SLOT(OpenFileBtn_Clicked()));
}connect(&SaveFileBtn, SIGNAL(clicked()), this, SLOT(SaveFileBtn_Clicked()));
}
}void Widget::SimpleMsgBtn_Clicked()
{
}QMessageBox msg(this);
38. }msg.setText("This is a message dialog!");
40. }msg.exec();
}
}void Widget::CustomMsgBtn_Clicked()
{
}QMessageBox msg(this);
47. }msg.setWindowTitle("Window Title");
}msg.setText("This is a detail message dialog!");
}msg.setIcon(QMessageBox::Information);
}msg.setStandardButtons(QMessageBox::Ok | QMessageBox::Cancel | QMessageBox::YesToAll);
52. }if( msg.exec() == QMessageBox::Ok )
}{
}qDebug() << "Ok button is clicked!";
}}
}
}void Widget::OpenFileBtn_Clicked()
{
}QFileDialog dlg(this);
62. }dlg.setAcceptMode(QFileDialog::AcceptOpen);
}dlg.setFilter("Text(*.txt)");
}dlg.setFileMode(QFileDialog::ExistingFiles);
66. }if( dlg.exec() == QFileDialog::Accepted )
}{
}QStringList fs = dlg.selectedFiles();
70. }for(int i=0; i<fs.count(); i++)
}{
}qDebug() << fs[i];
}}
}}
}
}void Widget::SaveFileBtn_Clicked()
{
}QFileDialog dlg(this);
81. }dlg.setAcceptMode(QFileDialog::AcceptSave);
}dlg.setFilter("Text(*.txt)");
}}if( dlg.exec() == QFileDialog::Accepted )
}{
}QStringList fs = dlg.selectedFiles();
89. }for(int i=0; i<fs.count(); i++)
}{
}qDebug() << fs[i];
}}
}}
}
}Widget::~Widget()
{
99. }
1. #ifndef _WIDGET_H_
2. #define _WIDGET_H_
3. #include <QtGui/QWidget>
#include <QPushButton>
}class Widget : public QWidget
{
}Q_OBJECT
10. private:
}QPushButton SimpleMsgBtn;
}QPushButton CustomMsgBtn;
}QPushButton OpenFileBtn;
}QPushButton SaveFileBtn;
15. private slots:
}void SimpleMsgBtn_Clicked();
}void CustomMsgBtn_Clicked();
}void OpenFileBtn_Clicked();
}void SaveFileBtn_Clicked();
20. public:
}Widget(QWidget *parent = 0);
}~Widget();
};
}#endif
