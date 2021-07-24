---
layout: post
title: Qt modelview (custom button)
category: qt5
tags: [qt5]
---
# 

## 

* effect

![ ](https://img-blog.csdn.net/20160324180552096)

QStyledItemDelegate

.h  Contains the smart pointer needed to display the button, the width and height of the button, the spacing between the buttons, the coordinates of the mouse, and so on.
    

1. class TableViewDelegate: public QStyledItemDelegate
    

2. {
    

3.  Q_OBJECT
    

4. 5. public:
    

6.  explicit TableViewDelegate(QWidget *parent = 0);
    

7.  ~TableViewDelegate();
    

8.  void paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const;
    

9.  bool editorEvent(QEvent* event, QAbstractItemModel* model, const QStyleOptionViewItem& option, const QModelIndex& index);
    

10. 11. signals:
    

12.  void open(const QModelIndex &index);
    

13.  void deleteData(const QModelIndex &index);
    

14. 15. private:
    

16.  QPoint m_mousePoint; // mouse position
    

17.  QScopedPointer<QPushButton> m_pOpenButton;
    

18.  QScopedPointer<QPushButton> m_pDeleteButton;
    

19.  QStringList m_list;
    

20.  Int m_nSpacing; // spacing between buttons
    

21.  Int m_nWidth; // button width
    

22.  Int m_nHeight; // button height
    

23.  Int m_nType; // button state-1: swipe 2: press
    

24. };
    
    

.cpp  Mainly set the button style, realize the mouse swipe, press, respond to mouse events and other operations.
    

1. TableViewDelegate::TableViewDelegate(QWidget *parent)
    

2.  : QStyledItemDelegate(parent),
    

3.  m_pOpenButton(new QPushButton()),
    

4.  m_pDeleteButton(new QPushButton()),
    

5.  m_nSpacing(5),
    

6.  m_nWidth(25),
    

7.  m_nHeight(20)
    

8. {
    

9.  // Set the button to normal, swipe, press the style
    

10.  m_pOpenButton->setStyleSheet("QPushButton {border: none; background-color: transparent; image:url(:/Images/open);} \
    

11.  QPushButton:hover {image:url(:/Images/openHover);} \
    

12.  QPushButton:pressed {image:url(:/Images/openPressed);}");
    

13. 14.  m_pDeleteButton->setStyleSheet("QPushButton {border: none; background-color: transparent; image:url(:/Images/delete);} \
    

15.  QPushButton:hover {image:url(:/Images/deleteHover);} \
    

16.  QPushButton:pressed {image:url(:/Images/deletePressed);}");
    

17.  M_list << QStringLiteral("Open") << QStringLiteral("Delete");
    

18. }
    

19. 20. TableViewDelegate::~TableViewDelegate()
    

21. {
    

22. 23. }
    

24. 25.  // draw button
    

26. void TableViewDelegate::paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const
    

27. {
    

28.  QStyleOptionViewItem viewOption(option);
    

29.  initStyleOption(&viewOption, index);
    

30.  if (option.state.testFlag(QStyle::State_HasFocus))
    

31.  viewOption.state = viewOption.state ^ QStyle::State_HasFocus;
    

32. 33.  QStyledItemDelegate::paint(painter, viewOption, index);
    

34. 35.  if (index.column() == FILE_OPERATE_COLUMN)
    

36.  {
    

37.  // Calculate the button display area
    

38.  int nCount = m_list.count();
    

39.  int nHalf = (option.rect.width() - m_nWidth * nCount - m_nSpacing * (nCount - 1)) / 2;
    

40.  int nTop = (option.rect.height() - m_nHeight) / 2;
    

41. 42.  for (int i = 0; i < nCount; ++i)
    

43.  {
    

44.  // draw button
    

45.  QStyleOptionButton button;
    

46.  button.rect = QRect(option.rect.left() + nHalf + m_nWidth * i + m_nSpacing * i,
    

47.  option.rect.top() + nTop, m_nWidth, m_nHeight);
    

48.  button.state |= QStyle::State_Enabled;
    

49.  //button.iconSize = QSize(16, 16);
    

50.  //button.icon = QIcon(QString(":/Images/%1").arg(m_list.at(i)));
    

51. 52.  if (button.rect.contains(m_mousePoint))
    

53.  {
    

54.  if (m_nType == 0)
    

55.  {
    

56.  button.state |= QStyle::State_MouseOver;
    

57.  //button.icon = QIcon(QString(":/Images/%1Hover").arg(m_list.at(i)));
    

58.  }
    

59.  else if (m_nType == 1)
    

60.  {
    

61.  button.state |= QStyle::State_Sunken;
    

62.  //button.icon = QIcon(QString(":/Images/%1Pressed").arg(m_list.at(i)));
    

63.  }
    

64.  }
    

65. 66.  QWidget *pWidget = (i == 0) ? m_pOpenButton.data() : m_pDeleteButton.data();
    

67.  QApplication::style()->drawControl(QStyle::CE_PushButton, &button, painter, pWidget);
    

68.  }
    

69.  }
    

70. }
    

71. 72.  // response button event - swipe, press
    

73. bool TableViewDelegate::editorEvent(QEvent* event, QAbstractItemModel* model, const QStyleOptionViewItem& option, const QModelIndex& index)
    

74. {
    

75.  if (index.column() != FILE_OPERATE_COLUMN)
    

76.  return false;
    

77. 78.  m_nType = -1;
    

79.  bool bRepaint = false;
    

80.  QMouseEvent *pEvent = static_cast<QMouseEvent *> (event);
    

81.  m_mousePoint = pEvent->pos();
    

82. 83.  int nCount = m_list.count();
    

84.  int nHalf = (option.rect.width() - m_nWidth * nCount - m_nSpacing * (nCount - 1)) / 2;
    

85.  int nTop = (option.rect.height() - m_nHeight) / 2;
    

86. 87.  // Restore mouse style
    

88.  QApplication::restoreOverrideCursor();
    

89. 90.  for (int i = 0; i < nCount; ++i)
    

91.  {
    

92.  QStyleOptionButton button;
    

93.  button.rect = QRect(option.rect.left() + nHalf + m_nWidth * i + m_nSpacing * i,
    

94.  option.rect.top() + nTop, m_nWidth, m_nHeight);
    

95. 96.  // The mouse is above the button
    

97.  if (!button.rect.contains(m_mousePoint))
    

98.  continue;
    

99. 100.  bRepaint = true;
    

101.  switch (event->type())
    

102.  {
    

103.  // The mouse rolls over
    

104.  case QEvent::MouseMove:
    

105.  {
    

106.  / / Set the mouse style to the hand type
    

107.  QApplication::setOverrideCursor(Qt::PointingHandCursor);
    

108. 109.  m_nType = 0;
    

110.  QToolTip::showText(pEvent->globalPos(), m_list.at(i));
    

111.  break;
    

112.  }
    

113.  // mouse down
    

114.  case QEvent::MouseButtonPress:
    

115.  {
    

116.  m_nType = 1;
    

117.  break;
    

118.  }
    

119.  // mouse release
    

120.  case QEvent::MouseButtonRelease:
    

121.  {
    

122.  if (i == 0)
    

123.  {
    

124.  emit open(index);
    

125.  }
    

126.  else
    

127.  {
    

128.  emit deleteData(index);
    

129.  }
    

130.  break;
    

131.  }
    

132.  default:
    

133.  break;
    

134.  }
    

135.  }
    

136. 137.  return bRepaint;
    

138. }