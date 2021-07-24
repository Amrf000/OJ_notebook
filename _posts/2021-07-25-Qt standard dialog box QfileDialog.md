---
layout: post
title: Qt standard dialog box QfileDialog
category: qt5
tags: [qt5]
---
# 

## 

* Add:
    
    public slots: void openDlg(); void saveDlg();
    

* 1

* 2

* 3

Constructor Add:
    
    MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent) { resize(600,600); QMenu *menu_F = menuBar()->addMenu(tr(File (& F) ")); QAction *openAction = new QAction(tr("turn on")); QIcon icon1(tr(":/image/open.ico")); openAction->setIcon(icon1); openAction->setShortcut(QKeySequence(tr("Ctrl+O"))); QAction *saveAction = new QAction(tr("save")); QIcon icon2(tr(":/image/save.ico")); saveAction->setIcon(icon2); saveAction->setShortcut(QKeySequence(tr("Ctrl+S"))); QAction *save_asAction = new QAction(tr("Save as")); QIcon icon3(tr(":/image/save_as.ico")); save_asAction->setIcon(icon3); save_asAction->setShortcut(QKeySequence(tr("Ctrl+A"))); menu_F->addAction(openAction); menu_F->addAction(saveAction); menu_F->addAction(save_asAction); QToolBar *file = addToolBar(tr("file")); file->addAction(openAction); file->addAction(saveAction); file->addAction(save_asAction); file->addSeparator();// increase the separator connect(openAction,&QAction::triggered,this,&MainWindow::openDlg); connect(saveAction,&QAction::triggered,this,&MainWindow::saveDlg); connect(save_asAction,&QAction::triggered,this,&MainWindow::saveDlg); }
    

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

openDlg
    
    void MainWindow::openDlg() { QString filename = QFileDialog::getOpenFileName(this,tr("turn on"),tr("C:"),tr("Image file (*.png *.JPG); Text file (*.txt)")); //QStringList filenames = QFileDialog::getOpenFileNames(this,tr("turn on"),tr("C:"),tr("Image file (*.png *.JPG); Text file (*.txt)")); //.... }
    

* 1

* 2

* 3

* 4

* 5

* 6

saveDlg
    
    void MainWindow::saveDlg() { QString savefile = QFileDialog::getSaveFileName(this,tr("save"),tr("unnamed"),tr("Image file (* .png * .jpg) ;; text file (* .txt)")); //..... }