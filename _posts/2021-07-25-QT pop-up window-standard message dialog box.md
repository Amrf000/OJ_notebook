---
layout: post
title: QT pop-up window-standard message dialog box
category: qt5
tags: [qt5]
---
* ### Article Directory
  * [Overview](https://www.programmersought.com/article/17855980570/#_2)
  * [Question message box](https://www.programmersought.com/article/17855980570/#Question_63)
  * [Information message box](https://www.programmersought.com/article/17855980570/#Information_93)
  * [Warning message box](https://www.programmersought.com/article/17855980570/#Warning_104)
  * [Critical message box](https://www.programmersought.com/article/17855980570/#Critical_115)
  * [About message box](https://www.programmersought.com/article/17855980570/#About_122)
  * [AboutQt message box](https://www.programmersought.com/article/17855980570/#AboutQt_131)
  * [to sum up](https://www.programmersought.com/article/17855980570/#_141)
## [Official document](https://doc.qt.io/qt-5/qmessagebox.html)Find the static member function of QMessageBox, you can see its function declaration.return valueFunction name and parameters
`void`[about](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent, const QString &title, const QString &text)
`void`[aboutQt](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent, const QString &title = QString())
`QMessageBox::StandardButton`[critical](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent,const QString &title,const QString &text,QMessageBox::StandardButtons buttons = Ok, QMessageBox::StandardButton defaultButton= NoButton)
`QMessageBox::StandardButton`[information](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent,const QString &title,const QString &text,QMessageBox::StandardButtons buttons = Ok,QMessageBox::StandardButton defaultButton= NoButton)
`QMessageBox::StandardButton`[question](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent,const QString &title,const QString &text,QMessageBox::StandardButtons buttons =StandardButtons(Yes&\#124No),QMessageBox::StandardButton defaultButton= NoButton)
`QMessageBox::StandardButton`[warning](https://doc.qt.io/qt-5/qmessagebox.html)(QWidget \*parent,const QString &title,const QString &text,QMessageBox::StandardButtons buttons = Ok,QMessageBox::StandardButton defaultButton= NoButton)
In general, the standard message dialog box QMessageBox class has six types of message boxes.Static functionFunction description
QMessageBox::questionQuestion message box
QMessageBox::informationInformation message box
QMessageBox::warningWarning message box
QMessageBox::criticalCritical message box
QMessageBox::aboutAbout message box
QMessageBox::aboutQtAboutQt message box
Standard button logo`QMessageBox::StandardButton`contentdescription
QMessageBox::Ok[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "OK" button.
QMessageBox::Open[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "open" button.
QMessageBox::Save[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "Save" button.
QMessageBox::Cancel[RejectRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Cancel" button.
QMessageBox::Close[RejectRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "close" button.
QMessageBox::Discard[DestructiveRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Discard" or "Do not save" button.
QMessageBox::Apply[ApplyRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Apply" button.
QMessageBox::Reset[ResetRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "reset" button.
QMessageBox::RestoreDefaults[ResetRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "Restore Defaults" button.
QMessageBox::Help[HelpRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Help" button.
QMessageBox::SaveAll[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Save All" button.
QMessageBox::Yes[YesRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Yes" button.
QMessageBox::YesToAll[YesRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Agree All" button.
QMessageBox::No[NoRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "No" button.
QMessageBox::NoToAll[NoRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "reject all" button.
QMessageBox::Abort[RejectRole](https://doc.qt.io/qt-5/qmessagebox.html)Defined "Abort" button.
QMessageBox::Retry[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "retry" button.
QMessageBox::Ignore[AcceptRole](https://doc.qt.io/qt-5/qmessagebox.html)The defined "ignore" button.
QMessageBox::NoButtonInvalid button.
Message severity![](/md_blog/public/assets/2021-07-25/67b25ce36608a913221117154ccf4ceb.png)[Question](https://doc.qt.io/qt-5/qmessagebox.html#Icon-enum)Used to ask questions during normal operation.
![](/md_blog/public/assets/2021-07-25/336450232cf38f4a06c61318cd9a0aec.png)[Information](https://doc.qt.io/qt-5/qmessagebox.html#Icon-enum)Used to report information about normal operations.
![](/md_blog/public/assets/2021-07-25/9d51dec371e684ec08ada2182460998f.png)[Warning](https://doc.qt.io/qt-5/qmessagebox.html#Icon-enum)Used to report non-critical errors.
![](/md_blog/public/assets/2021-07-25/972e04c08136157a06a5d4d0cfffc975.png)[Critical](https://doc.qt.io/qt-5/qmessagebox.html#Icon-enum)Used to report serious errors.
## [question](https://doc.qt.io/qt-5/qmessagebox.html)(`QWidget` \*parent,  
`const QString` &title,  
`const QString` &text,  
`QMessageBox::StandardButtons` buttons =StandardButtons(Yes|No),  
`QMessageBox::StandardButton` defaultButton= NoButton)
Sample code:
     QMessageBox::question(this, tr("Popup Title"), tr("Popup content"), QMessageBox::Ok | QMessageBox::Cancel, QMessageBox::Ok); 
effect:
![Question ](/md_blog/public/assets/2021-07-25/877f9f94ffdb49d8f2096192c7ac7e07.png)
Explanation:
* The fourth parameter buttons refers to the standard buttons to be added, set to`QMessageBox::Ok | QMessageBox::Cancel`Denotes adding confirmation key and cancel key.
* The fifth parameter defaultButton specifies to pressEnterThe button used when key, if it is`QMessageBox::NoButton`Then QMessageBox automatically selects an appropriate default value. .
* The function return type is`QMessageBox::StandardButton`, The return value can be used to know which button the user pressed, which can be used as the basis for subsequent operations.
## Information message box
The Information message box has the same parameters and return values ​​as the Question message box, and its usage and explanation are the same.
    QMessageBox::information(this, tr("Information message box title"), tr("This is the content of the Information message box."), QMessageBox::Ok | QMessageBox::Cancel, QMessageBox::Ok); 
![Information ](/md_blog/public/assets/2021-07-25/7ab0fe25d963a120bdae3126be40e090.png)
## Warning message box
The Warning message box is the same as above.
     QMessageBox::warning(this, tr("Warning message box"), tr("The content you modified has not been saved yet. Do you want to save the modification to the document?"), QMessageBox::Save | QMessageBox::Discard | QMessageBox::Cancel, QMessageBox::Save); 
![Warning ](/md_blog/public/assets/2021-07-25/685a5d6885c9012e980df18f85a84aa3.png)
## Critical message box
The Critical message box is the same as above.  
When calling, if the last two parameters are not specified, the button is set and the default button is set when pressed. The system will specify by default. (The above four message boxes are the same.)
    QMessageBox::critical(this, tr("Critical Message Box"), tr("This is a critical message box!")); 
![Critical ](/md_blog/public/assets/2021-07-25/e362dceee440d2e955a509dcd1966bf8.png)
## [about](https://doc.qt.io/qt-5/qmessagebox.html)(`QWidget` \*parent, `const QString` &title, `const QString` &text)
    QMessageBox::about(this, tr("About Message Box"), tr("This is an About message box test!")); 
![About ](/md_blog/public/assets/2021-07-25/9e29932e3adf759fec5574f89c40dfbf.png)
## [aboutQt](https://doc.qt.io/qt-5/qmessagebox.html)(`QWidget` \*parent, `const QString` &title = QString())
    QMessageBox::aboutQt(this, tr("About Qt Message Box")); 
![aboutQT.png](/md_blog/public/assets/2021-07-25/e2d07716d56d6072db70b7e18a7cad35.png)
## [text](https://doc.qt.io/qt-5/qmessagebox.html#text-prop), Used to further explain the alert or ask the user questions[Informational text](https://doc.qt.io/qt-5/qmessagebox.html#informativeText-prop), And an optional option to provide more data when the user needs it[Detailed text](https://doc.qt.io/qt-5/qmessagebox.html#detailedText-prop)。
