---
layout: post
title: Lesson 73-Multithreaded programming in Qt
category: qt5
tags: [qt5]
---
# 

## 

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
    

1. #include <QtCore/QCoreApplication>
    

2. #include <QThread>
    

3. #include <QDebug>
    

4. 5. class MyThread: public QThread //Create thread class
    

6. {
    

7. protected:
    

8.  void run() //Thread entry function
    

9.  {
    

10.  qDebug() << objectName() << " : " << "run() begin";
    

11. 12.  for(int i=0; i<5; i++)
    

13.  {
    

14.  qDebug() << objectName() << " : " << i;
    

15. 16.  sleep(1);
    

17.  }
    

18. 19.  qDebug() << objectName() << " : " << "run() end";
    

20.  }
    

21. };
    

22. 23.  int main(int argc, char *argv[]) //Main thread entry function
    

24. {
    

25.  QCoreApplication a(argc, argv);
    

26. 27.  qDebug() << "main() begin";
    

28. 29.  MyThread t; //Create child thread
    

30. 31.  t.setObjectName("t");
    

32. 33.  t.start(); //Start child thread
    

34. 35.  MyThread tt;
    

36. 37.  tt.setObjectName("tt");
    

38. 39.  tt.start();
    

40. 41.  for(int i=0; i<100000; i++)
    

42.  {
    

43.  for(int j=0; j<10000; j++)
    

44.  {
    

45. 			 //Delay
    

46.  }
    

47.  }
    

48. 49.  qDebug() << "main() end";
    

50. 51.  return a.exec();
    

52. }
    
    

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
    

1. #include <QtCore/QCoreApplication>
    

2. #include <QThread>
    

3. #include <QDebug>
    

4. 5. class Sample : public QThread
    

6. {
    

7. protected:
    

8.  volatile bool m_toStop;
    

9. 10.  void run()
    

11.  {
    

12.  qDebug() << objectName() << " : begin";
    

13. 14.  int* p = new int[10000];
    

15. 16.  for(int i=0; !m_toStop && (i<10); i++)
    

17.  {
    

18.  qDebug() << objectName() << " : " << i;
    

19. 20.  p[i] = i * i * i;
    

21. 22.  msleep(500);
    

23.  }
    

24. 25.  delete[] p;
    

26. 27.  qDebug() << objectName() << " : end";
    

28.  }
    

29. public:
    

30.  Sample()
    

31.  {
    

32.  m_toStop = false;
    

33.  }
    

34. 35.  void stop()
    

36.  {
    

37.  m_toStop = true;
    

38.  }
    

39. };
    

40. 41. int main(int argc, char *argv[])
    

42. {
    

43.  QCoreApplication a(argc, argv);
    

44. 45.  qDebug() << "main begin";
    

46. 47.  Sample t;
    

48. 49.  t.setObjectName("t");
    

50. 51.  t.start();
    

52. 53.  for(int i=0; i<100000; i++)
    

54.  {
    

55.  for(int j=0; j<10000; j++)
    

56.  {
    

57. 58.  }
    

59.  }
    

60. 61.  t.stop();
    

62.  //t.terminate();
    

63. 64.  qDebug() << "main end";
    

65. 66.  return a.exec();
    

67. }
    
    

No resource leaks anyway

4\. Summary

QThread is a cross-platform multi-thread solution

QThread implements multithreaded programming in a concise and easy-to-use manner

void run()Functions are used to implement thread execution bodies

void start()Start the thread and execute the run() function

Disabled in the projectvoid terminate()The function ends the thread

5、To be continued

.......