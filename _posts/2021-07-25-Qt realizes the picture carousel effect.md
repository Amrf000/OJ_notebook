---
layout: post
title: Qt realizes the picture carousel effect
category: qt5
tags: [qt5]
---
# 1\. Brief introduction

Today's article is about how to use Qt to achieve the effect of image carousel. In fact, we often see various advertisements on web pages that use image carousel to achieve the effect of embedding multiple advertisements in a small area.

The following are two common picture carousel effects on the CSDN page. Basically, it is to automatically switch the advertisement page regularly, or manually click to select the switch page.

In fact, it is not difficult to achieve, just use Qt's animation class to achieve similar effects. I made one before, but the effect was not good. I re-written it today and achieved an effect similar to the first one above. Through the Qt animation class to modify the transparency to achieve the switching effect of the upper and lower two pictures, the effect diagram is below.

![ ](/md_blog/public/assets/2021-07-25/7ffdc3b770c33471c69cec7a6cf20a15.gif) ![ ](/md_blog/public/assets/2021-07-25/086abc69013abb47e20dbe181c7d3916.gif)

# Second, the code path

After reading the above renderings, you can first think about the principles of its implementation. If you have an idea, you can implement it according to your own ideas first, and then look at the code in the article. If you have a better implementation idea before reading the article code, you can also comment and communicate with me. If you haven't thought of a good method, you can refer to the code in the article, if you have a problem or have an idea, call me.

I believe that everyone has their own unique ideas, so if you just look at the code in the article as soon as you come up, you may miss an opportunity to think, and you may lose a better idea. Haha, here is also onepersonal suggestion，The road to growth is step by step., Also myselfKeep thinking, keep summarizing, keep growingTo be able to be on this roadWalk steadily。

#### Tip

The realization principle is simply sorted out, mainly to provide the interface to set the path of the picture list, and then modify the transparency of the picture through the animation class to achieve the switching animation effect. And the picture is directly throughpaintEventEvents are drawn,Draw two pictures at the same time, first draw the next picture, and then draw the current picture according to the transparency returned by the animation class. The picture automatically switches through aclockCome get it done. Can alsoManually click the small white button to switch pictures。

Rewritten heremousePressEventEvent, we see the picture carousel on the web page, we can click on the current picture and then trigger the corresponding effect of each picture. Generally, it is a pop-up advertisement page. Here you can customize the function according to your needs.

Let's take a look at the realization of the picture carousel.

### CarouselImageWindow.h
    
    #include <QWidget> #include <QScrollArea> #include <QTimer> #include <QPropertyAnimation> #include <QPushButton> class CarouselImageWindow : public QWidget { Q_OBJECT public: CarouselImageWindow(QWidget *parent = NULL); ~CarouselImageWindow(); // Set the picture list; void setImageList(QStringList imageFileNameList); // add pictures; void addImage(QString imageFileName); // Start playing; void startPlay(); private: // Initialize the picture switch button; void initChangeImageButton(); // drawing event; void paintEvent(QPaintEvent *event); // mouse click event; void mousePressEvent(QMouseEvent* event); public slots: // Picture switching clock; void onImageChangeTimeout(); // Click on the picture switch button; void onImageSwitchButtonClicked(int buttonId); private: // Used for picture switching sliding effect, currently using transparency as the switching effect; QScrollArea* m_imagePlayWidget; // Picture list; QList<QString> m_imageFileNameList; // Picture switching clock; QTimer m_imageChangeTimer; // currently displayed image index; int m_currentDrawImageIndx; // switch picture; QPixmap m_currentPixmap; QPixmap m_nextPixmap; // Picture switching animation class; QPropertyAnimation* m_opacityAnimation; // Button list; QList<QPushButton*> m_pButtonChangeImageList; };
    

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

### Test code
    
    int main(int argc, char *argv[]) { QApplication a(argc, argv); CarouselImageWindow w; w.addImage(":/Resources/image1.jpg"); w.addImage(":/Resources/image2.jpg"); w.addImage(":/Resources/image3.jpg"); w.addImage(":/Resources/image4.jpg"); w.startPlay(); w.show(); return a.exec(); }
    

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

# tail

The article is over here. This article introduces the method of transparency to achieve the switching effect. The above mentioned another sliding effect, which can be used here.QScrollAreaTo achieve a similar effect, if I have time later, I will introduce how to achieve the sliding effect again in detail.

If you need specific project codes, please add the contact group on the left.