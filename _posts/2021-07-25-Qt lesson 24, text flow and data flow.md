---
layout: post
title: Qt lesson 24, text flow and data flow
category: qt5
tags: [qt5]
---
1\. File type
* Qt divides file types into two categories  
--- text file: the content of the file is readable text characters  
--- Data file: The content of the file is direct binary data
we know,QFile directly supports reading and writing of text files and data files  
![ ](/md_blog/public/assets/2021-07-25/32de7cca11faf50b9ae227f95cd1511d.png)  
Thinking: How to write a floating point data into a text file and a data file?
program:
    #include <QCoreApplication> #include <QFile> #include <QDebug> int main(int argc, char *argv[]) { QCoreApplication a(argc, argv); QFile file("C:/Users/xiebs/Desktop/test.hex"); if(file.open(QIODevice::WriteOnly)) { QString str = "D.T.SoftWare"; double value = 3.14; file.write(str.toStdString().c_str()); //Convert into byte data file.write(reinterpret_cast<char*>(&value), sizeof(value)); file.close(); } if(file.open(QIODevice::ReadOnly)) { QString str = ""; double value = 0; str = QString(file.read(12)); file.read(reinterpret_cast<char*>(&value), sizeof(value)); qDebug() << str; qDebug() << value; file.close(); } return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/f212b1545579792c66c3a929e384dff5.png)  
Conclusion: If you directly use QFile to read and write data or text, it is definitely feasible. The inconvenience lies in type conversion
2\. Text flow and data flow
* Qt provides auxiliary classes to simplify the reading and writing of text files/data files  
--- QTextStream: all written data is converted toReadable text  
--- QDataStream: The written data is converted toBinary data
* How to use IO device auxiliary class  
![ ](/md_blog/public/assets/2021-07-25/9aedb843025d9624e336cf9bf6ecbdc1.png)
3\. Version information of the data stream file
* The data stream file format of different Qt versions may be different  
--- `void setVersion(int v)`//Set the read and write version number  
--- `int version() const`//Get the read and write version number  
When the data stream file may transfer data between different versions of Qt programs, the version issue needs to be considered.
    #include <QCoreApplication> #include <QTextStream> #include <QDataStream> #include <QFile> #include <QDebug> void text_stream_test(QString str) { QFile file(str); if(file.open(QIODevice::WriteOnly | QIODevice::Text)) { QTextStream out(&file); out << "D.T.SoftWare" << endl; out << "xiebs" << endl; out << '5' << '*' << '6' << '=' << 5*6 << endl; file.close(); } if(file.open(QIODevice::ReadOnly | QIODevice::Text)) { QTextStream in(&file); while (!in.atEnd()) { QString line = in.readLine(); qDebug() << line; } file.close(); } } void data_stream_test(QString str) { QFile file(str); if(file.open(QIODevice::WriteOnly)) { QDataStream out(&file); out.setVersion(QDataStream::Qt_5_12); out << QString("D.T.SoftWare"); out << QString("Result"); out << 3.14; file.close(); } if(file.open(QIODevice::ReadOnly)) { QDataStream in(&file); QString str1 = ""; QString str2 = ""; double d = 0; in.setVersion(QDataStream::Qt_5_12); in >> str1; in >> str2; in >> d; qDebug() << str1; qDebug() << str2; qDebug() << d; file.close(); } } int main(int argc, char *argv[]) { QCoreApplication a(argc, argv); text_stream_test("C:/Users/xiebs/Desktop/test.text"); data_stream_test("C:/Users/xiebs/Desktop/test.dat"); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/42cb9f706ae058f5368c2762fea77eef.png)  
4\. Summary
* File auxiliary classes in Qt are used to facilitate read and write operations
* QTextStream is used for fast reading and writing of text data
* QDataStream is used for fast reading and writing of binary data
* The file format of QDataStream is related to the Qt version
* When the data format is transferred between programs, the version issue needs to be considered
