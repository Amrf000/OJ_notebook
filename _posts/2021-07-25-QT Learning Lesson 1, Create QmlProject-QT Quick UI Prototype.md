---
layout: post
title: QT Learning Lesson 1, Create QmlProject-QT Quick UI Prototype
category: qt5
tags: [qt5]
---
QT learning: Lesson 1, create QmlProject project-QT Quick UI Prototype
The purpose of this course: to learn the basic concepts of QML
Foreword: I have been engaged in the development of MFC, C \#, WPF for a long time. The reason for switching to QML is also to see the shortcomings of WPF, such as slow running speed, unable to run on embedded platforms, etc. Considering that the basic idea of ​​QML design is consistent with WPF, considering the rise of domestic systems in the future, decisively learn the cross-platform development of QT.
Step 1: Select the appropriate QT project creation type. In this lesson, directly select the QT Quick UI Prototype project, which is a pure QML project. You can run qmlscene to view the design results of qml. This study creates a project of Lesson1
The pure QML project can clearly divide the program design, which is more convenient for team software development
![](/md_blog/public/assets/2021-07-25/5a95d1afe85632bf106a328ed5855cfd.png)
![](/md_blog/public/assets/2021-07-25/c97fcb642c1cfe74ce061a0fe7a9ff94.png)
We see that QT automatically generated a Lesson1.qmlproject and Lesson1.qml project file
![](/md_blog/public/assets/2021-07-25/65cb88168c2ba86b5aae566059436d0e.png)
From the background script, we found that the entry of the program is the Lesson1.qml file
Step 2: Create a custom button MyButton.qml
1. import QtQuick 2.0
}Rectangle {
}id:myButton
}width:180
}height:50
}color: "green"
8. }Text {
}id: name
}text: qsTr("MyButton")
}}
13. }MouseArea {
}anchors.fill: parent
}onClicked: {
}if(name.text=="MyButton")
}name.text = "My mouse clicked!"
}else
}name.text="MyButton"
}}
}}
}
MyButton.qml is a custom control, see here, you can appreciate the great advantages of QT in software division. The use of Microsoft's MFC or C \# WPF or event definition is not as good as QT. We see that our custom MyButton can use Rectangle to define the button area, the internal text defines the button text, and MouseArea to define the event. The hierarchy and object division are very obvious.
Step 3: On the window of Lesson1.qml
![](/md_blog/public/assets/2021-07-25/0e44c89b1d91efcb62be12cf510beb1f.png)
