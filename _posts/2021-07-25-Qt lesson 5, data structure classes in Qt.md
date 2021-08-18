---
layout: post
title: Qt lesson 5, data structure classes in Qt
category: qt5
tags: [qt5]
---
* 1\. The queue in C++
Achieve aFirst in first out The data structure is aTemplate class. head File `#include <queue>`
Usage (take int type as an example):
    queue<int> Q; 　　　　//Define an int type queue Q.empty(); 　　//return whether the queue is empty Q.size(); //Returns the current queue length Q.front(); //Returns the first element of the current queue Q.back(); //Return the last element of the current queue Q.push(); 　　 　//Insert an element at the end of the queue, such as inserting the number 5: Q.push(5) Q.pop(); //From the current queue, remove the first element 
Code example:
    #include <iostream> #include <queue> using namespace std; int main() { queue<int> Q; cout<<"queue empty: " << Q.empty() << endl; for(int i = 0; i < 5; i++) { Q.push(i); //Into the queue } cout << "queue empty: " << Q.empty() << endl; cout << "queue size: " << Q.size() << endl; cout << endl; for(int i = 0; i < 5; i++) { cout << "queue front: "<< Q.front() << endl; Q.pop(); //out of the queue } return 0; } 
![ ](https://img-blog.csdnimg.cn/20191205102429487.png)
-QQueue in QT
Its parent is`QList`, Is a template class. head File: `#include <QQueue>`
Common usage (take int type as an example):
    QQueue<int> Q; 　　　　 //Define an int type queue Q.isEmpty(); //return whether the queue is empty Q.size(); //Returns the number of queue elements Q.clear(); //Empty the queue Q.enqueue(); //Add an element to the end of the queue, such as inserting the number 5: Q.enqueue(5) Q.dequeue(); //Delete the first element of the current queue and return this element Q.head(); //Returns the first element of the current queue Q.last(); //Returns the element at the end of the current queue T& operator[]( int i ); //Access queue elements in array form 
Code example:
    #include <QApplication> #include <QQueue> #include <QDebug> int main(int argc,char * argv[]) { QQueue<int> Q; //Define an int type queue qDebug() << "queue empty: "<< Q.isEmpty(); //returns whether the queue is empty for(int i = 0; i < 5; i++) { Q.enqueue(i); //Enqueue } qDebug() << "queue empty: " << Q.isEmpty(); qDebug() << "queue size: " << Q.size(); for(int i = 0; i < 5; i++) { 	 qDebug() << "queue last: "<< Q.last(); //Returns the last element of the current queue 	 qDebug() << "queue head: "<< Q.dequeue(); //Leave the queue and return the first element of the current queue } qDebug() << "queue empty: " << Q.isEmpty(); qDebug() << "queue size: " << Q.size(); return 0; } 
print:
    queue empty: true queue empty: false queue size: 5 queue last: 4 queue head: 0 queue last: 4 queue head: 1 queue last: 4 queue head: 2 queue last: 4 queue head: 3 queue last: 4 queue head: 4 queue empty: true queue size: 0 
2\. Stack in C++
Achieve aFirst in last out The data structure is a template class. In the intel system, the stack grows downward, the header file`#include <stack>`
Usage (take int type as an example):
    stack <int> s; 　　　　　　　　　 //Define an int type stack s.empty(); //Whether the return stack is empty s.size(); //Returns the number of elements in the current stack s.push(); //Pile an element on top of the stack s.pop(); //Delete the element on the top of the stack s.top(); //returns the element at the top of the stack and will not delete it 
Code example:
    #include <iostream> #include <stack> using namespace std; int main() { stack<int> s; cout << "stack empty: " << s.empty() << endl; for(int i = 0; i < 5; i++) { s.push(i); //Push into the stack } cout << "stack empty: " << s.empty() << endl; cout << "stack size: " << s.size() << endl; cout << endl; for(int i = 0; i < 5; i++) { cout << "stack top: " << s.top() << endl; s.pop(); //pop the stack } return 0; } 
![ ](https://img-blog.csdnimg.cn/20191205103904992.png)  
QStack in QT
head File `#include < QStack >`
Common usage (take int type as an example):
    QStack <int> s; 　　　 //Define an int type stack s. isEmpty(); 　　 // Whether the return stack is empty s.size(); //Returns the number of elements in the current stack s.push(); //Pile an element on top of the stack s.pop(); //Delete the element on the top of the stack and return this element s.top(); //returns the element at the top of the stack and will not delete it T & operator[] (int i ); 　　 //Access queue elements in array form 
Code example:
    #include <QApplication> #include <QStack> #include <QDebug> int main(int argc,char * argv[]) { QStack <int> s; //Define an int type stack qDebug() << "Stack empty: "<< s.isEmpty(); //Returns whether the stack is empty for(int i = 0;i < 5; i++) { s.push(i); //Push into the stack } qDebug() << "Stack empty: " << s.isEmpty(); qDebug() << "Stack size: " << s.size(); for(int i = 0; i < 5; i++) { qDebug() << "Stack top: "<< s.pop(); //pop the stack and view the first element on the top of the current stack } qDebug() << "Stack empty: " << s.isEmpty(); qDebug() << "Stack size: " << s.size(); return 0; } 
run:
    Stack empty: true Stack empty: false Stack size: 5 Stack top: 4 Stack top: 3 Stack top: 2 Stack top: 1 Stack top: 0 Stack empty: true Stack size: 0
