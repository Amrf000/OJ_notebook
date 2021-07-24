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
#include <QtCore/QCoreApplication>
#include <QThread>
#include <QDebug>
}class MyThread: public QThread //Create thread class
{
7. protected:
}void run() //Thread entry function
}{
}qDebug() << objectName() << " : " << "run() begin";
11. }for(int i=0; i<5; i++)
}{
}qDebug() << objectName() << " : " << i;
15. }sleep(1);
}}
18. }qDebug() << objectName() << " : " << "run() end";
}}
};
22. }int main(int argc, char *argv[]) //Main thread entry function
{
}QCoreApplication a(argc, argv);
26. }qDebug() << "main() begin";
28. }MyThread t; //Create child thread
30. }t.setObjectName("t");
32. }t.start(); //Start child thread
34. }MyThread tt;
36. }tt.setObjectName("tt");
38. }tt.start();
40. }for(int i=0; i<100000; i++)
}{
}for(int j=0; j<10000; j++)
}{
45. 			 //Delay
}}
}}
48. }qDebug() << "main() end";
50. }return a.exec();
}
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
------ Add flag variable in thread classm\_toStop (volatile bool) 
------ Passedm\_toStopDetermines whether it needs to be returned from the run() function
3\. Programming experiment
Elegant thread control 73-2.pro
main.cpp
#include <QtCore/QCoreApplication>
#include <QThread>
#include <QDebug>
}class Sample : public QThread
{
7. protected:
}volatile bool m_toStop;
9. }void run()
}{
}qDebug() << objectName() << " : begin";
13. }int* p = new int[10000];
15. }for(int i=0; !m_toStop && (i<10); i++)
}{
}qDebug() << objectName() << " : " << i;
19. }p[i] = i * i * i;
21. }msleep(500);
}}
24. }delete[] p;
26. }qDebug() << objectName() << " : end";
}}
29. public:
}Sample()
}{
}m_toStop = false;
}}
34. }void stop()
}{
}m_toStop = true;
}}
};
}int main(int argc, char *argv[])
{
}QCoreApplication a(argc, argv);
44. }qDebug() << "main begin";
46. }Sample t;
48. }t.setObjectName("t");
50. }t.start();
52. }for(int i=0; i<100000; i++)
}{
}for(int j=0; j<10000; j++)
}{
57. }}
}}
60. }t.stop();
}//t.terminate();
63. }qDebug() << "main end";
65. }return a.exec();
}
No resource leaks anyway
4\. Summary
QThread is a cross-platform multi-thread solution
QThread implements multithreaded programming in a concise and easy-to-use manner
void run()Functions are used to implement thread execution bodies
void start()Start the thread and execute the run() function
Disabled in the projectvoid terminate()The function ends the thread
5、To be continued
.......