---
layout: post
title: Use Qt to achieve a simple picture preview effect
category: qt5
tags: [qt5]
---
# 

Qt simplifies the development of the UI interface. Compared with MFC, it is faster to get started and advanced; this article mainly explains the function of using QListWidget to load pictures and arrange them and set the background picture of the main window;

The interface effect is as shown in the figure below: the top two rows are pre-loaded thumbnails, click a single thumbnail to set the corresponding picture as the background picture of the main window

![](/public/assets/2021-07-25/e914d28d0c6905e3bccef70d05dfaa9e.JPEG)

The main code is as follows, the constructor function of the main window (generate widgets and load content):

[?](https://www.cnblogs.com/#)

//Constructor

MainWindow::MainWindow(QWidget \*parent): QMainWindow(parent)

{

//Create QListWidget widget

m\_pListWidget = new QListWidget(this);

//Set the picture size of the unit item in QListWidget

m\_pListWidget-&gt;setIconSize(QSize(W\_ICONSIZE, H\_ICONSIZE));

m\_pListWidget-&gt;setResizeMode(QListView::Adjust);

//Set the display mode of QListWidget

m\_pListWidget-&gt;setViewMode(QListView::IconMode);

//Set the unit item in QListWidget cannot be dragged

m\_pListWidget-&gt;setMovement(QListView::Static);

//Set the spacing of the unit items in QListWidget

m\_pListWidget-&gt;setSpacing(10);

//Create 11 unit items in sequence

for(int nIndex = 0;nIndex<11;++nIndex)

{

//Get picture path

QString strPath=QString(":/list/image/%1.jpg").arg(nIndex+1);

//Generate image objPixmap

QPixmap objPixmap(strPath);

//Generate a QListWidgetItem object (note: its Icon image is scaled \[96\*96\]) ---scaled function

QListWidgetItem \*pItem = new QListWidgetItem(QIcon(objPixmap.scaled(QSize(W\_ICONSIZE,H\_ICONSIZE))),"animal tiger pig");

//Set the width and height of the unit item

pItem-\>setSizeHint(QSize(W\_ICONSIZE,H\_ITEMSIZE));

m\_pListWidget-&gt;insertItem(nIndex, pItem);

}

setCentralWidget(m\_pListWidget);

//Set the signal slot

connect(m\_pListWidget,SIGNAL(itemClicked(QListWidgetItem\*)),this,SLOT(Slot\_ItemClicked(QListWidgetItem\*)));

m\_strPath = "";

setWindowTitle("www.hnmade.com");

}

The code to set the background image of the window is as follows:

[?](https://www.cnblogs.com/#)

//Set the background of the main window

void MainWindow::SetBgImage(const QString &strPath)

{

QPixmap objPixmap(strPath);

QPalette palette = this-&gt;palette();

if(strPath.isEmpty())

{

palette.setBrush(QPalette::Base, QBrush(QColor(0,0,255)));

}

else

{

palette.setBrush(QPalette::Base, QBrush(objPixmap.scaled(width(),height())));

}

setPalette(palette);

}

×××Address: http://files.cnblogs.com/appsucc/ListWidgetImage.rar

Reprinted at: https://blog.51cto.com/515632/791799