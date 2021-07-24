---
layout: post
title: Qt custom agent class
category: qt5
tags: [qt5]
---
* ## Example
![](/md_blog/public/assets/2021-07-25/5883e255a0217626e0ae50be4b2c1ca6.png)
From the above figure, you can see age is an INT type, so you can use QspinBox as an editing component.
## Customize the basic design requirements of the agency class
![](/md_blog/public/assets/2021-07-25/8f1365c80ba0ed8bea443768f7dacf31.png)
QABSTractItemdeLegate is an abstract base class for all proxy classes.
QStylediteMdelegate is the default proxy class used by the view component, and QItemDelegate is also a similar function class.
QStyledItemdeLegate and QiteMdeLegate distinguish between QStyledItemDelegate can use the current style sheet setting to draw components, so it is recommended to use qstyleditemdelegate.
Also have to implement the following functions
* CreateEditor (): Create a Widget component used to edit model data, such as QspinBox, QComboBox.
* SetEditRData (): Get data from the data model for editing for Widget components.
* SetModeldata (): Update the data on the Widget to the data model.
* UpdateEditorGeometry (): It is used to set a suitable size to the Widget component.
### Custom agent based on QspinBox
1. //.h
2. #ifndef SPINBOXDELEGATE_H
3. #define SPINBOXDELEGATE_H
4. #include <QStyledItemDelegate>
#include <QWidget>
#include <QModelIndex>
#include <QSpinBox>
}class SpinBoxDelegate : public QStyledItemDelegate
{
}Q_OBJECT
13. public:
}explicit SpinBoxDelegate(QObject *parent = nullptr);
15. }QWidget *createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const;
17. }void setEditorData(QWidget *editor, const QModelIndex &index) const;
19. }void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const;
21. }void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const;
};
}#endif // SPINBOXDELEGATE_H
1. //.cpp
#include "SpinBoxDelegate.h"
}SpinBoxDelegate::SpinBoxDelegate(QObject *parent) : QStyledItemDelegate(parent)
{
6. }
}QWidget *SpinBoxDelegate::createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
}QSpinBox *editor = new QSpinBox(parent);
12. }// Set boundless box
}editor->setFrame(false);
15. }// Set the minimum value
}editor->setMinimum(0);
18. }// Set the maximum value
}editor->setMaximum(100);
21. }//return
}return editor;
}
}void SpinBoxDelegate::setEditorData(QWidget *editor, const QModelIndex &index) const
{
}int value = index.model()->data(index,Qt::EditRole).toInt();
}QSpinBox *spinBox = static_cast<QSpinBox*>(editor);
}spinBox->setValue(value);
}
}void SpinBoxDelegate::setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
{
}QSpinBox *spinBox = static_cast<QSpinBox*>(editor);
}spinBox->interpretText();
}int value = spinBox->value();
}model->setData(index,value,Qt::EditRole);
}
}void SpinBoxDelegate::updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
}editor->setGeometry(option.rect);
}
use
    ui->tableView->setItemDelegateForColumn(2,&delegate);
operation result
![](/md_blog/public/assets/2021-07-25/99f0454c577abe3102f7a116f85100cd.png)
## Complete source code
[https://download.csdn.net/download/wzz953200463/15453057](https://download.csdn.net/download/wzz953200463/15453057)