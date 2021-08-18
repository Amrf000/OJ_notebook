---
layout: post
title: Lesson 73-Multithreaded programming in Qt
category: qt5
tags: [qt5]
---
1\. Multithreaded programming in Qt  
Qt directly supports multithreading through QThread
- QThreadIs a cross-platform multi-thread solution
- QThreadMultithreaded programming in a simple and easy way
![](/md_blog/public/assets/2021-07-25/78dd9fb75df024b62f59fcd0cb18e068.png)
Key member functions in QThread
- void run() 
Thread Thread function, used to define thread function (execution flow)
- void start() 
   Start function,Set the thread entry address to the run function
- void terminate() 
  ★ End the thread forcibly (not recommended)
Programming example
![](/md_blog/public/assets/2021-07-25/27947e9781c36d30b3f0a9d771a96616.png)
In the example, the main thread will end before the child thread
After all the threads are finished, the process is finished.
2\. Programming experiment
A preliminary exploration of multi-threaded programming 73-1.pro
main.cpp
```
#include <QDebug>
#include <QThread>
#include <QtCore/QCoreApplication>

class MyThread : public QThread {
protected:
  void run() {
    qDebug() << objectName() << "run() begin";

    for (int i = 0; i < 5; i++) {
      qDebug() << objectName() << i;
      sleep(1);
    }
    qDebug() << objectName() << "run() end";
  }
};

int main(int argc, char *argv[]) {
  QCoreApplication a(argc, argv);
  qDebug() << "main() begin";

  MyThread t1;
  t1.setObjectName("t1");
  t1.start();

  MyThread t2;
  t2.setObjectName("t2");
  t2.start();

  qDebug() << "main() end";
  return a.exec();
}

Create multiple threads
```
![](/md_blog/public/assets/2021-07-25/0132bb66e8ad6d53e7bac4cb9348239b.png)
Multiple threads execute in parallel
Thread life cycle
![](/md_blog/public/assets/2021-07-25/a83afc477181293e94ac03151acd15d2.png)
Focus on
In engineering development[terminate()](https://blog.csdn.net/qq_39654127/article/details/81329085)Is prohibited, Terminate() will
So that the operating system violently terminates the thread without considering data integrity,
Issues such as resource release! A
How to terminate threads gracefully in code? A
Solution ideas
－The end of the run() function execution is the only way to terminate the thread gracefully
------ Add flag variable in thread classm_toStop (volatile bool) 
------ Passedm_toStopDetermines whether it needs to be returned from the run() function
3. Programming experiment
Elegant thread control 73-2.pro
main.cpp
```
#include <QDebug>
#include <QThread>
#include <QtCore/QCoreApplication>

class Sample : public QThread {
protected:
  volatile bool m_toStop;

  void run() {
    qDebug() << objectName() << " : begin";

    int *p = new int[10000];

    for (int i = 0; !m_toStop && (i < 10); i++) {
      qDebug() << objectName() << " : " << i;

      p[i] = i * i * i;

      msleep(500);
    }

    delete[] p;

    qDebug() << objectName() << " : end";
  }

public:
  Sample() { m_toStop = false; }

  void stop() { m_toStop = true; }
};

int main(int argc, char *argv[]) {
  QCoreApplication a(argc, argv);

  qDebug() << "main begin";

  Sample t;

  t.setObjectName("t");

  t.start();

  for (int i = 0; i < 100000; i++) {
    for (int j = 0; j < 10000; j++) {
    }
  }

  t.stop();
  // t.terminate();//If the violence ends, a memory leak will occur in this
  // case, and the space pointed to by the p pointer is not destroyed

  qDebug() << "main end";

  return a.exec();
}

Ending violently and gracefully
```
No resource leaks anyway
4. Summary
QThread is a cross-platform multi-thread solution
QThread implements multithreaded programming in a concise and easy-to-use manner
void run()Functions are used to implement thread execution bodies
void start()Start the thread and execute the run() function
Disabled in the projectvoid terminate()The function ends the thread
5、To be continued
.......
