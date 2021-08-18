---
layout: post
title: Use of QT5 mac QtXlsxWriter
category: qt5
tags: [qt5]
---
I studied QtXlsxWriter's reading and writing of xlsx, and shared the process of writing here:
    git clone https://github.com/VSRonin/QtXlsxWriter.git
1. cd QtXlsxWriter
2. qmake
3. make -j8
4. sudo make install
Then the installation was successful.
Then open Qtcreated and create a QT project. Plus:
    QT += xlsx
Then in my mainwindows.cpp the following:
```
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QMessageBox>
#include <QtXlsx>
}
MainWindow::MainWindow(QWidget *parent) :
}
QMainWindow(parent),
}
ui(new Ui::MainWindow) {}
ui->setupUi(this);
}
QXlsx::Document xlsx;
}
xlsx.write("A1", "Hello Qt!");
}
xlsx.saveAs("/Users/eric/Documents/qt_projects/Test.xlsx");
}
}
}
MainWindow::~MainWindow() {}
delete ui;
}
```
When the operation is completed, you will find that there is one more Test.xlsx in the qt\_projects directory. If you want to know more functions, please refer to the following documents.
# references
\[1\]. VSRonin/QtXlsxWriter. [https://github.com/VSRonin/QtXlsxWriter](https://github.com/VSRonin/QtXlsxWriter)
\[2\]. Qt Xlsx. [http://qtxlsx.debao.me/](http://qtxlsx.debao.me/)
