---
layout: post
title: [Qt] implement picture sliding effect
category: qt5
tags: [qt5]
---
Show results:  
![ ](/md_blog/public/assets/2021-07-25/8733c8cee9ed5ddb87133a831c2e5409.png)  
Code  
.h file
    
    #ifndef MAINWINDOW_H #define MAINWINDOW_H #include <QMainWindow> #define IMAGE_WIDTH 300 #define IMAGE_HEIGHT 200 #if _MSC_VER >= 1600 #pragma execution_character_set("utf-8") #endif QT_BEGIN_NAMESPACE namespace Ui { class MainWindow; } QT_END_NAMESPACE class MainWindow : public QMainWindow { Q_OBJECT public: MainWindow(QWidget *parent = nullptr); ~MainWindow(); QStringList getImageFilePath(const QString&); private slots: void on_lineEdit_textChanged(const QString &arg1); void cellClickedEvent(int, int); private: Ui::MainWindow *ui; QStringList img_list; }; #endif // MAINWINDOW_H 
    

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

.c file
    
    #include "mainwindow.h" #include "ui_mainwindow.h" #include <QScroller> #include <QDir> #include <QLabel> #include <QPixmap> #include <QDebug> #include <QListWidget> MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent) , ui(new Ui::MainWindow) { ui->setupUi(this); ui->tableWidget->verticalHeader()->hide(); ui->tableWidget->horizontalHeader()->hide(); ui->tableWidget->setRowCount(1); QSize size = QSize(IMAGE_WIDTH, IMAGE_HEIGHT); ui->tableWidget->setRowHeight(0, size.height()); ui->tableWidget->setHorizontalScrollBarPolicy(Qt::ScrollBarAlwaysOff); ui->tableWidget->setVerticalScrollBarPolicy(Qt::ScrollBarAlwaysOff); ui->tableWidget->setHorizontalScrollMode(QListWidget::ScrollPerPixel); QScroller::grabGesture(ui->tableWidget,QScroller::LeftMouseButtonGesture); connect(ui->tableWidget, &QTableWidget::cellClicked, this, &MainWindow::cellClickedEvent); img_list = getImageFilePath("../img"); } MainWindow::~MainWindow() { delete ui; } void MainWindow::on_lineEdit_textChanged(const QString &arg1) { if(arg1.isEmpty()) return; int count = arg1.toInt(); if(count > img_list.count()) count = img_list.count(); ui->tableWidget->clear(); ui->tableWidget->setColumnCount(count); for (int i = 0; i < count; i++) { ui->tableWidget->setColumnWidth(i, IMAGE_WIDTH); QLabel *label = new QLabel; QImage image(img_list.at(i)); label->setPixmap(QPixmap::fromImage(image.scaled(IMAGE_WIDTH, IMAGE_HEIGHT, Qt::KeepAspectRatioByExpanding))); ui->tableWidget->setCellWidget(0,i,label); } } void MainWindow::cellClickedEvent(int row, int col) { Q_UNUSED(row) qDebug() << col; } QStringList MainWindow::getImageFilePath(const QString &dirpath) { QDir dir(dirpath); QStringList files_path; files_path.clear(); if(!dir.exists()) return files_path; QStringList nameFilters; nameFilters << "*.png" << "*.jpg"; QStringList files_name = dir.entryList(nameFilters, QDir::Files | QDir::Readable, QDir::Name); for (int i = 0; i < files_name.size(); i++) { files_path << dirpath + "/" + files_name.at(i); } return files_path; } 
    

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

* 54

* 55

* 56

* 57

* 58

* 59

* 60

* 61

* 62

* 63

* 64

* 65

* 66

* 67

* 68

* 69

* 70

* 71

* 72

* 73

* 74

* 75

* 76

* 77

* 78

* 79

* 80

* 81

* 82

* 83

UI layout  
![ ](/md_blog/public/assets/2021-07-25/82ac528f7f65b68b2acc306a993f6869.png)