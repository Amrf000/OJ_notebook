---
layout: post
title: Qt lesson 8, the parent-child relationship between Qt objects
category: qt5
tags: [qt5]
---
1\. The relationship between Qt objects
* There can be a parent-child relationship between Qt objects  
--- Each object holds pointers to all its child objects  
--- Every object has a pointer to its parent  
![ ](/md_blog/public/assets/2021-07-25/a05b0a6405abdcd64cff5a32ba5ff7f4.png)
* When specifying the parent of a Qt object  
--- its parent object will beChild object linked listPointer to the object  
--- The object will save a pointer to its parent  
![ ](/md_blog/public/assets/2021-07-25/ccb1e44263906b76b6cf44020238d5e0.png)
    #include <QCoreApplication> #include <QDebug> void fcTest() { QObject* p = new QObject(); QObject* c1 = new QObject(); QObject* c2 = new QObject(); c1->setParent(p); c2->setParent(p); qDebug() << "c1 = " << c1; qDebug() << "c2 = " << c2; const QObjectList& list = p->children(); //Linked list object for(int i = 0;i < list.length();i++) { qDebug() << list[i]; } qDebug() << "p: " << p; qDebug() << "c1 parent: " << c1->parent(); qDebug() << "p2 parent: " << c2->parent(); } int main(int argc, char *argv[]) { QCoreApplication a(argc, argv); fcTest(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/bcd0239732a4734902933846ee1953a0.png)
* When the Qt object is destroyed  
--- remove yourself from the Children List of the parent object  
--- destroy all objects in your Children List
What is a Qt object: (Define a class that inherits from QObject, so the resulting object is called Qt object)
Note: When developing with Qt, not only must always pay attention to the problem of memory leakage, but also always pay attention to whether the object may be destroyed multiple times
* Use the parent-child relationship between Qt objects to form an object tree
* Deleting a node in the tree will cause the corresponding subtree to be destroyed  
![ ](/md_blog/public/assets/2021-07-25/db435191be7da2b0e930d0203ffb1919.png)
    #include <QCoreApplication> #include <QDebug> class MObj :public QObject { private: QString m_name; public: MObj(const QString& name ) { m_name = name; qDebug() << "construct:" << m_name; } ~MObj() { qDebug() << "destruct:" << m_name; } }; void delTest() { MObj* obj1 = new MObj("obj1"); MObj* obj2 = new MObj("obj2"); MObj* obj3 = new MObj("obj3"); MObj* obj4 = new MObj("obj4"); obj2->setParent(obj1); obj4->setParent(obj3); obj3->setParent(obj1); delete obj3; qDebug() << "Obj2:" << obj2; const QObjectList& List = obj1->children(); for(int i = 0;i<List.length();i++) { qDebug() << List[i]; } } int main(int argc, char *argv[]) { QCoreApplication a(argc, argv); delTest(); return a.exec(); } 
![ ](/md_blog/public/assets/2021-07-25/bbb71b408f8ea1cc0ab5b9cac69b4f42.png)
summary:
* There can be a parent-child relationship between Qt objects
* The Qt object tree can be obtained through the parent-child relationship
* Release the parent-child relationship with the parent object when the Qt object is destroyed
* When the Qt object is destroyed, all child objects will be destroyed at the same time