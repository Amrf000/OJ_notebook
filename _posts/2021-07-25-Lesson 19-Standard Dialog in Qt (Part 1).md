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
    

1. #include <QtGui/QApplication>
    

2. #include "Widget.h"
    

3. 4. int main(int argc, char *argv[])
    

5. {
    

6.  QApplication a(argc, argv);
    

7.  Widget w;
    

8. 9.  w.show();
    

10. 11.  return a.exec();
    

12. }
    
    


1. #include "Widget.h"
    

2. #include <QDebug>
    

3. #include <QMessageBox>
    

4. #include <QFileDialog>
    

5. 6. 7. Widget::Widget(QWidget *parent) : QWidget(parent),
    

8.  SimpleMsgBtn(this), CustomMsgBtn(this), OpenFileBtn(this), SaveFileBtn(this)
    

9. {
    

10.  SimpleMsgBtn.setText("Simple Message Dialog");
    

11.  SimpleMsgBtn.move(20, 20);
    

12.  SimpleMsgBtn.resize(160, 30);
    

13. 14.  CustomMsgBtn.setText("Custom Message Dialog");
    

15.  CustomMsgBtn.move(20, 70);
    

16.  CustomMsgBtn.resize(160, 30);
    

17. 18.  OpenFileBtn.setText("Open File Dialog");
    

19.  OpenFileBtn.move(20, 120);
    

20.  OpenFileBtn.resize(160, 30);
    

21. 22.  SaveFileBtn.setText("Save File Dialog");
    

23.  SaveFileBtn.move(20, 170);
    

24.  SaveFileBtn.resize(160, 30);
    

25. 26.  resize(200, 220);
    

27.  setFixedSize(200, 220);
    

28. 29.  connect(&SimpleMsgBtn, SIGNAL(clicked()), this, SLOT(SimpleMsgBtn_Clicked()));
    

30.  connect(&CustomMsgBtn, SIGNAL(clicked()), this, SLOT(CustomMsgBtn_Clicked()));
    

31.  connect(&OpenFileBtn, SIGNAL(clicked()), this, SLOT(OpenFileBtn_Clicked()));
    

32.  connect(&SaveFileBtn, SIGNAL(clicked()), this, SLOT(SaveFileBtn_Clicked()));
    

33. }
    

34. 35. void Widget::SimpleMsgBtn_Clicked()
    

36. {
    

37.  QMessageBox msg(this);
    

38. 39.  msg.setText("This is a message dialog!");
    

40. 41.  msg.exec();
    

42. }
    

43. 44. void Widget::CustomMsgBtn_Clicked()
    

45. {
    

46.  QMessageBox msg(this);
    

47. 48.  msg.setWindowTitle("Window Title");
    

49.  msg.setText("This is a detail message dialog!");
    

50.  msg.setIcon(QMessageBox::Information);
    

51.  msg.setStandardButtons(QMessageBox::Ok | QMessageBox::Cancel | QMessageBox::YesToAll);
    

52. 53.  if( msg.exec() == QMessageBox::Ok )
    

54.  {
    

55.  qDebug() << "Ok button is clicked!";
    

56.  }
    

57. }
    

58. 59. void Widget::OpenFileBtn_Clicked()
    

60. {
    

61.  QFileDialog dlg(this);
    

62. 63.  dlg.setAcceptMode(QFileDialog::AcceptOpen);
    

64.  dlg.setFilter("Text(*.txt)");
    

65.  dlg.setFileMode(QFileDialog::ExistingFiles);
    

66. 67.  if( dlg.exec() == QFileDialog::Accepted )
    

68.  {
    

69.  QStringList fs = dlg.selectedFiles();
    

70. 71.  for(int i=0; i<fs.count(); i++)
    

72.  {
    

73.  qDebug() << fs[i];
    

74.  }
    

75.  }
    

76. }
    

77. 78. void Widget::SaveFileBtn_Clicked()
    

79. {
    

80.  QFileDialog dlg(this);
    

81. 82.  dlg.setAcceptMode(QFileDialog::AcceptSave);
    

83.  dlg.setFilter("Text(*.txt)");
    

84. 85. 86.  if( dlg.exec() == QFileDialog::Accepted )
    

87.  {
    

88.  QStringList fs = dlg.selectedFiles();
    

89. 90.  for(int i=0; i<fs.count(); i++)
    

91.  {
    

92.  qDebug() << fs[i];
    

93.  }
    

94.  }
    

95. }
    

96. 97. Widget::~Widget()
    

98. {
    

99. 100. }
    
    


1. #ifndef _WIDGET_H_
    

2. #define _WIDGET_H_
    

3. 4. #include <QtGui/QWidget>
    

5. #include <QPushButton>
    

6. 7. class Widget : public QWidget
    

8. {
    

9.  Q_OBJECT
    

10. private:
    

11.  QPushButton SimpleMsgBtn;
    

12.  QPushButton CustomMsgBtn;
    

13.  QPushButton OpenFileBtn;
    

14.  QPushButton SaveFileBtn;
    

15. private slots:
    

16.  void SimpleMsgBtn_Clicked();
    

17.  void CustomMsgBtn_Clicked();
    

18.  void OpenFileBtn_Clicked();
    

19.  void SaveFileBtn_Clicked();
    

20. public:
    

21.  Widget(QWidget *parent = 0);
    

22.  ~Widget();
    

23. };
    

24. 25. #endif