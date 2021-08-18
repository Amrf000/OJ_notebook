---
layout: post
title: Qt modelview (custom button)
category: qt5
tags: [qt5]
---
* effect
![ ](https://img-blog.csdn.net/20160324180552096)
QStyledItemDelegate
.h  Contains the smart pointer needed to display the button, the width and height of the button, the spacing between the buttons, the coordinates of the mouse, and so on.
1. class TableViewDelegate: public QStyledItemDelegate
{
}Q_OBJECT
}public:
}explicit TableViewDelegate(QWidget *parent = 0);
}~TableViewDelegate();
}void paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const;
}bool editorEvent(QEvent* event, QAbstractItemModel* model, const QStyleOptionViewItem& option, const QModelIndex& index);
}signals:
}void open(const QModelIndex &index);
}void deleteData(const QModelIndex &index);
}private:
}QPoint m_mousePoint; // mouse position
}QScopedPointer<QPushButton> m_pOpenButton;
}QScopedPointer<QPushButton> m_pDeleteButton;
}QStringList m_list;
}Int m_nSpacing; // spacing between buttons
}Int m_nWidth; // button width
}Int m_nHeight; // button height
}Int m_nType; // button state-1: swipe 2: press
};
.cpp  Mainly set the button style, realize the mouse swipe, press, respond to mouse events and other operations.
1. TableViewDelegate::TableViewDelegate(QWidget *parent)
}: QStyledItemDelegate(parent),
}m_pOpenButton(new QPushButton()),
}m_pDeleteButton(new QPushButton()),
}m_nSpacing(5),
}m_nWidth(25),
}m_nHeight(20)
{
}// Set the button to normal, swipe, press the style
}m_pOpenButton->setStyleSheet("QPushButton {border: none; background-color: transparent; image:url(:/Images/open);} \
}QPushButton:hover {image:url(:/Images/openHover);} \
}QPushButton:pressed {image:url(:/Images/openPressed);}");
13. }m_pDeleteButton->setStyleSheet("QPushButton {border: none; background-color: transparent; image:url(:/Images/delete);} \
}QPushButton:hover {image:url(:/Images/deleteHover);} \
}QPushButton:pressed {image:url(:/Images/deletePressed);}");
}M_list << QStringLiteral("Open") << QStringLiteral("Delete");
}
}TableViewDelegate::~TableViewDelegate()
{
22. }
24. }// draw button
26. void TableViewDelegate::paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
}QStyleOptionViewItem viewOption(option);
}initStyleOption(&viewOption, index);
}if (option.state.testFlag(QStyle::State_HasFocus))
}viewOption.state = viewOption.state ^ QStyle::State_HasFocus;
32. }QStyledItemDelegate::paint(painter, viewOption, index);
34. }if (index.column() == FILE_OPERATE_COLUMN)
}{
}// Calculate the button display area
}int nCount = m_list.count();
}int nHalf = (option.rect.width() - m_nWidth * nCount - m_nSpacing * (nCount - 1)) / 2;
}int nTop = (option.rect.height() - m_nHeight) / 2;
41. }for (int i = 0; i < nCount; ++i)
}{
}// draw button
}QStyleOptionButton button;
}button.rect = QRect(option.rect.left() + nHalf + m_nWidth * i + m_nSpacing * i,
}option.rect.top() + nTop, m_nWidth, m_nHeight);
}button.state |= QStyle::State_Enabled;
}//button.iconSize = QSize(16, 16);
}//button.icon = QIcon(QString(":/Images/%1").arg(m_list.at(i)));
51. }if (button.rect.contains(m_mousePoint))
}{
}if (m_nType == 0)
}{
}button.state |= QStyle::State_MouseOver;
}//button.icon = QIcon(QString(":/Images/%1Hover").arg(m_list.at(i)));
}}
}else if (m_nType == 1)
}{
}button.state |= QStyle::State_Sunken;
}//button.icon = QIcon(QString(":/Images/%1Pressed").arg(m_list.at(i)));
}}
}}
65. }QWidget *pWidget = (i == 0) ? m_pOpenButton.data() : m_pDeleteButton.data();
}QApplication::style()->drawControl(QStyle::CE_PushButton, &button, painter, pWidget);
}}
}}
}
71. }// response button event - swipe, press
73. bool TableViewDelegate::editorEvent(QEvent* event, QAbstractItemModel* model, const QStyleOptionViewItem& option, const QModelIndex& index)
{
}if (index.column() != FILE_OPERATE_COLUMN)
}return false;
77. }m_nType = -1;
}bool bRepaint = false;
}QMouseEvent *pEvent = static_cast<QMouseEvent *> (event);
}m_mousePoint = pEvent->pos();
82. }int nCount = m_list.count();
}int nHalf = (option.rect.width() - m_nWidth * nCount - m_nSpacing * (nCount - 1)) / 2;
}int nTop = (option.rect.height() - m_nHeight) / 2;
86. }// Restore mouse style
}QApplication::restoreOverrideCursor();
89. }for (int i = 0; i < nCount; ++i)
}{
}QStyleOptionButton button;
}button.rect = QRect(option.rect.left() + nHalf + m_nWidth * i + m_nSpacing * i,
}option.rect.top() + nTop, m_nWidth, m_nHeight);
95. }// The mouse is above the button
}if (!button.rect.contains(m_mousePoint))
}continue;
99. }bRepaint = true;
}switch (event->type())
}{
}// The mouse rolls over
}case QEvent::MouseMove:
}{
}/ / Set the mouse style to the hand type
}QApplication::setOverrideCursor(Qt::PointingHandCursor);
108. }m_nType = 0;
}QToolTip::showText(pEvent->globalPos(), m_list.at(i));
}break;
}}
}// mouse down
}case QEvent::MouseButtonPress:
}{
}m_nType = 1;
}break;
}}
}// mouse release
}case QEvent::MouseButtonRelease:
}{
}if (i == 0)
}{
}emit open(index);
}}
}else
}{
}emit deleteData(index);
}}
}break;
}}
}default:
}break;
}}
}}
136. }return bRepaint;
}
