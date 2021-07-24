---
layout: post
title: Lesson 31, Introduction to Software Development Process
category: qt5
tags: [qt5]
---
# 1\. Software development process
1\. What is the software development process
(1), through a series of steps to ensure the smooth completion of the software product
(2) Management methodology of software products during the life cycle
2\. The essence of the software development process
(1) The development process has nothing to do with specific technology
(2) The development process is a rule that the development team must follow
3\. Common software development process
(1), improvisation model (Build-and-Fix Model)
A. Start development immediately after communicating with end users
B. There is no need analysis and demand discovery process
C. There is no overall design and planning process
D. There is no relevant software documentation and poor maintainability
(2) Waterfall Model
A. The core idea of ​​the waterfall model is to simplify the problem according to the process, separate the realization of the function from the design, and facilitate the division of labor and cooperation, that is, the use of structured analysis and design methods to separate the logical realization from the physical realization.
B. Divide the software life cycle into six basic activities: planning, demand analysis → software design → program writing → software testing → release, operation and maintenance, and stipulate their top-down, fixed sequence of interconnection, like a waterfall Flowing water, falling step by step.
C. Provide checkpoints divided by stages for the project. After the current stage is completed, just focus on the subsequent stages.
D. Since the development steps are linear and irreversible, users can only see the development results until the end of the entire process, which increases development risks.
(3), incremental model (Incremental Model)
A. The system function is decomposed into non-overlapping sub-functions. It introduces the concept of incremental packages. You don't need to wait until all the requirements are released. Development can be carried out as long as the incremental package of a certain requirement is released. Although a certain incremental package may need to be further adapted to the needs of the customer and changed, as long as the incremental package is small enough, its impact can be bearable for the entire project.
B. Fully implement one sub-function each time. Since only part of the user's functions are submitted each time, users have more time to learn and adapt to new products.
C. The incremental model combines the basic components (repetitive application) of the waterfall model and the iterative features of the prototype implementation. The model uses linear sequences that are staggered as the schedule progresses, and each linear sequence produces a releaseable "increment" of the software. When using the incremental model, the first incremental is often the core product, that is, the first incremental achieves the basic requirements, but many supplementary features have not been released. The customer's use and evaluation of each incremental release is regarded as the new feature and function of the next incremental release. This process is repeated after each incremental release until the final perfect product is produced.
D. After all the sub-functions are completed, the system development ends.
![](/md_blog/public/assets/2021-07-25/efae4ea0ad492c4321c3031e8e8d7cbb.JPEG)
(4) Spiral Model
A. Adopt an iterative method for system development, which combines the waterfall model and the rapid prototyping model.
B. The software project is broken down into multiple different versions to complete
C. The development process of each version requires user participation
D. Plan the next version based on the feedback of the previous version
E. The risk-driven spiral model is suitable for large-scale software projects developed internally, but only when the developers have experience and expertise in risk analysis and risk elimination can the use of this model be successful.
![](/md_blog/public/assets/2021-07-25/88a1854cceeece43dcad7aded70e2749.png)
(5) Agile Modeling
![](/md_blog/public/assets/2021-07-25/76dd160e3a5dd41eaa39b9ac74c7a0d7.JPEG) 
A. Keep everything simple
B. Embrace change
C. Work efficiently
D. Continuous development
4\. Incremental model is suitable for the development of text editors
(1) Relatively fixed demand
(2) Weak coupling between functions
![](/md_blog/public/assets/2021-07-25/9e6490d00db35fbe5859e222e5686548.JPEG) 
NotePad.pro project phase test (for memory leak detection: valgrind tool)
![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.h
1. #ifndef MAINWINDOW_H
2. #define MAINWINDOW_H
#include <QMenuBar>
#include <QMenu>
#include <QAction>
#include <QString>
#include <QtGui/QMainWindow>
#include <QToolBar>
#include <QIcon>
#include <QSize>
1#include <QStatusBar>
#include <QLabel>
#include <QPlainTextEdit>
14. class MainWindow : public QMainWindow
{
}Q_OBJECT
17. private:
}QPlainTextEdit mainEdit;
}QLabel statusLabel;
}MainWindow(QWidget *parent = 0);
}MainWindow(const MainWindow& obj);
}MainWindow* operator = (const MainWindow& obj);
}bool construct();
24. }bool initMenuBar();//Menu bar
}bool initToolBar();//Toolbar
}bool initStatusBar();//Status bar
}bool initinitMainEditor();//Edit window
29. }bool initFileMenu(QMenuBar* mb);//File menu
}bool initEditMenu(QMenuBar* mb);//Edit menu
}bool initFormatMenu(QMenuBar* mb);//Format menu
}bool initViewMenu(QMenuBar* mb);//View menu
}bool initHelpMenu(QMenuBar* mb);//Help menu
35. }bool initFileToolItem(QToolBar* tb);//Tool options
}bool initEditToolItem(QToolBar* tb);
}bool initFormatToolItem(QToolBar* tb);
}bool initViewToolItem(QToolBar* tb);
}}bool makeAction(QAction*& action,QMenu* menu, QString text, int key);//menu item
}bool makeAction(QAction*& action,QToolBar* tb, QString tip, QString icon);
44. public:
}static MainWindow* NewInstance();
}~MainWindow();
};
}#endif // MAINWINDOW_H
}MainWindow.h
![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.cpp
#include "MainWindow.h"
#include <QDebug>
}MainWindow::MainWindow(QWidget *parent)
}: QMainWindow(parent), statusLabel(this)
{
}
}bool MainWindow::construct()
{
}bool ret = true;
}ret = ret && initMenuBar();
}ret = ret && initToolBar();
}ret = ret && initStatusBar();
}ret = ret && initinitMainEditor();
}return ret;
}
18. MainWindow* MainWindow::NewInstance()
{
}MainWindow* ret = new MainWindow();
21. }if((ret==NULL) || (!ret->construct()))
}{
}delete ret;
}ret = NULL;
}}
27. }return ret;
}
}bool MainWindow::initMenuBar()//Menu bar
{
}bool ret = true;
33. }QMenuBar* mb = menuBar();//Be sure to pay attention to menuBar(), which is an ordinary member function, not a constructor
35. }ret = ret && initFileMenu(mb);//Passing a parameter is to add the menu to the menu bar in the initFileMenu() function
}ret = ret && initEditMenu(mb);
}ret = ret && initFormatMenu(mb);
}ret = ret && initViewMenu(mb);
}ret = ret && initHelpMenu(mb);
41. }return ret;
43. }
45. }bool MainWindow::initToolBar()//Toolbar
{
}bool ret = true;
49. }QToolBar* tb = addToolBar("Tool Bar");
}//tb->setMovable(false);
}//tb->setFloatable(false);
}tb->setIconSize(QSize(16,16));
54. }ret = ret && initFileToolItem(tb);
}tb->addSeparator();
}ret = ret && initEditToolItem(tb);
}tb->addSeparator();
}ret = ret && initFormatToolItem(tb);
}tb->addSeparator();
}ret = ret && initViewToolItem(tb);
62. }return ret;
}
65. }bool MainWindow::initStatusBar()//Status bar
{
}bool ret = true;
69. }QStatusBar* sb = statusBar();
71. }QLabel* label = new QLabel("Made By LGC");
73. }if(label != NULL)
}{
}statusLabel.setMinimumWidth(200);
}statusLabel.setAlignment(Qt::AlignHCenter);
}statusLabel.setText("Ln:1 Col:1");
}}label->setMinimumWidth(200);
}label->setAlignment(Qt::AlignHCenter);
83. }sb->addPermanentWidget(new QLabel());//Just add the separator
}sb->addPermanentWidget(&statusLabel);
}sb->addPermanentWidget(label);
}}
}else
}{
}ret = false;
}}
}return ret;
}
}bool MainWindow::initinitMainEditor()//Edit window
{
}bool ret = true;
97. }mainEdit.setParent(this);
}setCentralWidget(&mainEdit);
100. }return ret;
}
103. }/************************************************file menu************************************************* *******/
105. bool MainWindow::initFileMenu(QMenuBar* mb)
{
}bool ret = true;
108. }QMenu* menu = new QMenu("File(&F)");//Create a file menu, (&F) is to open it with Alt+F
}ret = (menu != NULL);
}if(ret)
}{
}QAction* action = NULL;
114. }//New
}ret = ret && makeAction(action, menu, "New(&N)",Qt::CTRL + Qt::Key_N);
}if(ret)
}{
}menu->addAction(action);
}}
121. }menu->addSeparator();
123. }//Open
}ret = ret && makeAction(action, menu,"Open(&O)...",Qt::CTRL + Qt::Key_O);
}if(ret)
}{
}menu->addAction(action);
}}
130. }menu->addSeparator();
132. }//Save
}ret = ret && makeAction(action, menu,"Save(&S)",Qt::CTRL + Qt::Key_S);
}if(ret)
}{
}menu->addAction(action);
}}
139. }menu->addSeparator();
141. }//Save As
}ret = ret && makeAction(action, menu, "Save As(&A)...",0);
}if(ret)
}{
}menu->addAction(action);
}}
148. }menu->addSeparator();
150. }//print
}ret = ret && makeAction(action, menu, "Print(&P)...",Qt::CTRL + Qt::Key_P);
}if(ret)
}{
}menu->addAction(action);
}}
157. }menu->addSeparator();
159. }//Exit
}ret = ret && makeAction(action, menu,"Exit(&X)",0);
}if(ret)
}{
}menu->addAction(action);//Add menu items to the menu
}}
166. }}
}if(ret)
}{
}mb->addMenu(menu);//Add the menu to the menu bar
}}
}else
}{
}delete mb;
}}
}return ret;
}
178. }/************************************************edit menu************************************************* *******/
180. bool MainWindow::initEditMenu(QMenuBar* mb)
{
}bool ret = true;
183. }QMenu* menu = new QMenu("Edit(&E)");
}ret = (menu != NULL);
}if(ret)
}{
}QAction* action = NULL;
189. }//Undo
}ret = ret && makeAction(action, menu,"Undo(&U)",Qt::CTRL + Qt::Key_Z);
}if(ret)
}{
}menu->addAction(action);
}}
196. }menu->addSeparator();
198. }//Redo
}ret = ret && makeAction(action, menu,"Redo(&R)...",Qt::CTRL + Qt::Key_Y);
}if(ret)
}{
}menu->addAction(action);
}}
205. }menu->addSeparator();
207. }//Cut
}ret = ret && makeAction(action, menu,"Cut(&T)",Qt::CTRL + Qt::Key_X);
}if(ret)
}{
}menu->addAction(action);
}}
214. }menu->addSeparator();
216. }//Copy
}ret = ret && makeAction(action, menu,"Copy(&C)...",Qt::CTRL + Qt::Key_C);
}if(ret)
}{
}menu->addAction(action);
}}
223. }menu->addSeparator();
225. }//Pase
}ret = ret && makeAction(action, menu,"Pase(&P)...",Qt::CTRL + Qt::Key_V);
}if(ret)
}{
}menu->addAction(action);
}}
232. }menu->addSeparator();
234. }//Delete
}ret = ret && makeAction(action, menu, "Delete(&L)",Qt::Key_Delete);
}if(ret)
}{
}menu->addAction(action);
}}
241. }menu->addSeparator();
243. }//Find
}ret = ret && makeAction(action, menu,"Find(&F)...",Qt::CTRL + Qt::Key_F);
}if(ret)
}{
}menu->addAction(action);
}}
250. }menu->addSeparator();
252. }//Replace
}ret = ret && makeAction(action, menu,"Replace(&R)...",Qt::CTRL + Qt::Key_H);
}if(ret)
}{
}menu->addAction(action);
}}
259. }menu->addSeparator();
261. }//Goto
}ret = ret && makeAction(action, menu,"Goto(&G)",Qt::CTRL + Qt::Key_G);
}if(ret)
}{
}menu->addAction(action);
}}
268. }menu->addSeparator();
270. }//Select All
}ret = ret && makeAction(action, menu, "Select All(&A)",Qt::CTRL + Qt::Key_A);
}if(ret)
}{
}menu->addAction(action);
}}
277. }}
}if(ret)
}{
}mb->addMenu(menu);
}}
}else
}{
}delete mb;
}}
}return ret;
}
289. }/************************************************format menu************************************************* *******/
291. bool MainWindow::initFormatMenu(QMenuBar* mb)
{
}bool ret = true;
294. }QMenu* menu = new QMenu("Format(&O)");
}ret = (menu != NULL);
}if(ret)
}{
}QAction* action = NULL;
300. }//Auto Wrap
}ret = ret && makeAction(action, menu,"Auto Wrap(&W)",0);
}if(ret)
}{
}menu->addAction(action);
}}
307. }menu->addSeparator();
309. }//Font
}ret = ret && makeAction(action, menu,"Font(&F)...",0);
}if(ret)
}{
}menu->addAction(action);
}}
316. }}
}if(ret)
}{
}mb->addMenu(menu);
}}
}else
}{
}delete mb;
}}
}return ret;
}
328. }/************************************************view menu************************************************* *******/
330. bool MainWindow::initViewMenu(QMenuBar* mb)
{
}bool ret = true;
333. }QMenu* menu = new QMenu("View(&V)");
}ret = (menu != NULL);
}if(ret)
}{
}QAction* action = NULL;
339. }//Tool Bar
}ret = ret && makeAction(action, menu,"Tool Bar(&T)",0);
}if(ret)
}{
}menu->addAction(action);
}}
346. }menu->addSeparator();
348. }//Status Bar
}ret = ret && makeAction(action, menu,"Status Bar(&S)",0);
}if(ret)
}{
}menu->addAction(action);
}}
355. }}
}if(ret)
}{
}mb->addMenu(menu);
}}
}else
}{
}delete mb;
}}
}return ret;
}
367. }/************************************************help menu************************************************* *******/
369. bool MainWindow::initHelpMenu(QMenuBar* mb)
{
}bool ret = true;
372. }QMenu* menu = new QMenu("Help(&H)");
}ret = (menu != NULL);
}if(ret)
}{
}QAction* action = NULL;
378. }//User Manual
}ret = ret && makeAction(action, menu,"User Manual",0);
}if(ret)
}{
}menu->addAction(action);
}}
385. }menu->addSeparator();
387. }//About NotePad
}ret = ret && makeAction(action, menu,"About NotePad...",0);
}if(ret)
}{
}menu->addAction(action);
}}
394. }}
}if(ret)
}{
}mb->addMenu(menu);
}}
}else
}{
}delete mb;
}}
}return ret;
}
}/*****************************************tool******* ************************************************** ***/
407. bool MainWindow::initFileToolItem(QToolBar* tb)
{
}bool ret = true;
}QAction* action = NULL;
411. }ret = ret && makeAction(action, tb, "New", ":/Res/pic/new.png");
}if(ret)
}{
}tb->addAction(action);
416. }}
418. }ret = ret && makeAction(action, tb,"Open", ":/Res/pic/open.png");
}if(ret)
}{
}tb->addAction(action);
}}
424. }ret = ret && makeAction(action, tb,"Save", ":/Res/pic/save.png");
}if(ret)
}{
}tb->addAction(action);
}}
430. }ret = ret && makeAction(action, tb,"Save As", ":/Res/pic/saveas.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Print", ":/Res/pic/print.png");
}if(ret)
}{
}tb->addAction(action);
}}
}return ret;
442. }
444. bool MainWindow::initEditToolItem(QToolBar* tb)
{
}bool ret = true;
}QAction* action = NULL;
448. }ret = ret && makeAction(action, tb,"Undo", ":/Res/pic/undo.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Redo", ":/Res/pic/redo.png");
}if(ret)
}{
}tb->addAction(action);
}}
459. }ret = ret && makeAction(action, tb, "Cut", ":/Res/pic/cut.png");
}if(ret)
}{
}tb->addAction(action);
}}
465. }ret = ret && makeAction(action, tb,"Copy", ":/Res/pic/copy.png");
}if(ret)
}{
}tb->addAction(action);
}}
471. }ret = ret && makeAction(action, tb,"Paste", ":/Res/pic/paste.png");
}if(ret)
}{
}tb->addAction(action);
}}
477. }ret = ret && makeAction(action, tb,"Find", ":/Res/pic/find.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Replace", ":/Res/pic/replace.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Goto", ":/Res/pic/goto.png");
}if(ret)
}{
}tb->addAction(action);
}}
493. }return ret;
}
496. bool MainWindow::initFormatToolItem(QToolBar* tb)
{
}bool ret = true;
}QAction* action = NULL;
500. }ret = ret && makeAction(action, tb, "Auto Wrap", ":/Res/pic/wrap.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Font", ":/Res/pic/font.png");
}if(ret)
}{
}tb->addAction(action);
}}
511. }return ret;
}
514. bool MainWindow::initViewToolItem(QToolBar* tb)
{
}bool ret = true;
}QAction* action = NULL;
518. }ret = ret && makeAction(action, tb,"Tool Bar", ":/Res/pic/tool.png");
}if(ret)
}{
}tb->addAction(action);
}}
}ret = ret && makeAction(action, tb,"Status Bar", ":/Res/pic/status.png");
}if(ret)
}{
}tb->addAction(action);
}}
529. }return ret;
}
}}bool MainWindow::makeAction(QAction*& action,QMenu* menu, QString text, int key)//menu item
{
}bool ret = true;
}action = new QAction(text, menu);
}if(action != NULL)
}{
}action->setShortcut(QKeySequence(key));//Create shortcut key
}}
}else
}{
}ret = false;
}}
546. }return ret;
}
549. bool MainWindow::makeAction(QAction*& action,QToolBar* tb, QString tip, QString icon)
{

}bool ret = true;


}action = new QAction("", tb);


}if(action != NULL)


}{


}action->setToolTip(tip);


}action->setIcon(QIcon(icon));


}}


}else


}{


}ret = false;


}}


}return ret;


}


564. MainWindow::~MainWindow()


{


566. }


}MainWindow.cpp



![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) main.cpp


#include <QtGui/QApplication>


#include "MainWindow.h"


3. int main(int argc, char *argv[])


{


}QApplication a(argc, argv);


}MainWindow* w = MainWindow::NewInstance();


}int ret = -1;


}if(w != NULL)


}{


}w->show();


}ret = a.exec();


}}


13. }delete w;


}return ret;


}


}main.cpp



# 2\. Summary

(1) The software development process is a series of rules followed by the development team

(2) The significance of the software development process is to ensure the quality and progress of the product

(3) A variety of development process models already exist in the industry

(4) Each software development process has a specific scope of application

(5) The incremental model is used in the curriculum for project development