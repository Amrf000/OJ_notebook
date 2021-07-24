---
layout: post
title: Qt Custom delegate class. Subclass QStyledItemDelegate
category: qt5
tags: [qt5]
---
# 

## 

* Since the sub-items of QListWidget are all single-column. So there is not much that can be displayed, but if you use the listWidget-\>setItemWidget(); method, the memory overhead is a bit large. So there are some information that can be drawn by drawing, First look at the simple effect:

![ ](/public/assets/2021-07-25/5270fa91de1153c37286d6d7131246db.gif)

Like QListWidget, QTableWidget, these all belong to the view class. The default has a basic Delegate. When we want to give more display methods to the children of the view, we can subclass QStyledItemDelegate or QItemDelegate, and we can subclass QStyledItemDelegate below. As an example:
    
    #ifndef MYITEMDELEGATE_H #define MYITEMDELEGATE_H #include <QStyledItemDelegate> #include <QPainter> //Subclassed delegate class. class MyItemDelegate : public QStyledItemDelegate { Q_OBJECT public: MyItemDelegate(QWidget *parent); ~MyItemDelegate(); protected: //Rewrite these two virtual functions. Note: constDon't forget, otherwise it does not belong to the rewriting of virtual functions. virtual QSize sizeHint(const QStyleOptionViewItem & option, const QModelIndex & index) const; virtual void paint(QPainter * painter, const QStyleOptionViewItem & option, const QModelIndex & index) const; private: }; #endif // MYITEMDELEGATE_H 
    

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

    #include "MyItemDelegate.h" MyItemDelegate::MyItemDelegate(QWidget *parent) : QStyledItemDelegate(parent) { } MyItemDelegate::~MyItemDelegate() { } //The method of adjusting the size needs to be rewritten. Note: The size of the sub-item is adjusted. QSize MyItemDelegate::sizeHint(const QStyleOptionViewItem & option, const QModelIndex & index) const { //Get the original view parameters. QSize size = QStyledItemDelegate::sizeHint(option, index); size.setHeight(80); return size; } void MyItemDelegate::paint(QPainter * painter, const QStyleOptionViewItem & option, const QModelIndex & index) const { //Return the rectangular border of the item. QRect rect = option.rect; //When the item is selected. if (option.state & QStyle::State_Selected) { painter->setBrush(Qt::cyan); painter->drawRect(rect); } //Get the data of the item. QString name = index.data(Qt::DisplayRole).toString(); QString phone = index.data(Qt::UserRole).toString(); QString address = index.data(Qt::UserRole + 1).toString(); //Draw the name. painter->drawText(rect.topLeft() + QPoint(20, 20), QString::fromLocal8Bit("Name: %1").arg(name)); //Draw the phone. painter->drawText(rect.topLeft() + QPoint(20, 40), QString::fromLocal8Bit("Phone: %1").arg(phone)); //Draw address. painter->drawText(rect.topLeft() + QPoint(20, 60), QString::fromLocal8Bit("Address 1").arg(address)); }
    

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

    #include "c.h" c::c(QWidget *parent) : QWidget(parent) { ui.setupUi(this); m_precRow = -1; //First add four data items. addItem("test1", "100000000000",QString::fromLocal8Bit("Beijing")); addItem("test2", "100000000001", QString::fromLocal8Bit("Hangzhou")); addItem("test3", "100000000002", QString::fromLocal8Bit("Xiamen")); addItem("test4", "100000000003", QString::fromLocal8Bit("Shanghai")); //The signal emitted when the item is clicked. connect(ui.listWidget, SIGNAL(itemClicked(QListWidgetItem*)), this, SLOT(detailDisplaySlot(QListWidgetItem*))); } c::~c() { } void c::addItem(QString name, QString phone, QString address) { //Create item. QListWidgetItem *item = new QListWidgetItem(); //Set the data of the item. item->setData(Qt::DisplayRole,name); item->setData(Qt::UserRole, phone); item->setData(Qt::UserRole + 1, address); //Set the size of the item. item->setSizeHint(QSize(ui.listWidget->width(),40)); ui.listWidget->addItem(item); } void c::detailDisplaySlot(QListWidgetItem* item) { //When the clicked item is changed, the previous item's delegation needs to be changed. Also change the size. if (m_precRow >= 0) { ui.listWidget->setItemDelegateForRow(m_precRow, new QStyledItemDelegate()); ui.listWidget->item(m_precRow)->setSizeHint(QSize(ui.listWidget->width(), 40)); } //Get the number of rows of the clicked item. m_precRow = ui.listWidget->row(item); //Set the current line of the clicked item to use the delegate defined by yourself. ui.listWidget->setItemDelegateForRow(ui.listWidget->row(item), new MyItemDelegate(ui.listWidget)); //Reset the size. ui.listWidget->item(m_precRow)->setSizeHint(QSize(ui.listWidget->size().width(),80)); } 
    

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

    #ifndef C_H #define C_H #include <QtWidgets/QWidget> #include "ui_c.h" #include "MyItemDelegate.h" class c : public QWidget { Q_OBJECT public: c(QWidget *parent = 0); ~c(); void addItem(QString,QString,QString); private slots: void detailDisplaySlot(QListWidgetItem*); private: Ui::cClass ui; int m_precRow = -1; }; #endif // C_H 
    

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

In this way, you are done. Of course, the listWidget-\>setItemWidget(); method can also achieve such a scenario, but if the number of subitems is very large, the memory overhead is very large!