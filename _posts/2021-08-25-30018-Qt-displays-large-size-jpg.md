---
layout: post
title: Qt displays large size jpg
category: qt
tags: [qt]
---

Qt displays large size jpg(https://www.qtcentre.org/threads/30018-Qt-displays-large-size-jpg)
[](/biteme/)

[![Qt Centre Forum](images/qtcentre/QtCentre.png "Qt Centre Forum")](forum.php)

*   [Register](register.php)
*   [Help](faq.php)
*      
    
     Remember Me?
    
        
    
    YAHOO.util.Dom.setStyle('navbar\_password\_hint', "display", "inline"); YAHOO.util.Dom.setStyle('navbar\_password', "display", "none"); vB\_XHTML\_Ready.subscribe(function() { // YAHOO.util.Event.on('navbar\_username', "focus", navbar\_username\_focus); YAHOO.util.Event.on('navbar\_username', "blur", navbar\_username\_blur); YAHOO.util.Event.on('navbar\_password\_hint', "focus", navbar\_password\_hint); YAHOO.util.Event.on('navbar\_password', "blur", navbar\_password); }); function navbar\_username\_focus(e) { // var textbox = YAHOO.util.Event.getTarget(e); if (textbox.value == 'User Name') { // textbox.value=''; textbox.style.color='#000000'; } } function navbar\_username\_blur(e) { // var textbox = YAHOO.util.Event.getTarget(e); if (textbox.value == '') { // textbox.value='User Name'; textbox.style.color='#777777'; } } function navbar\_password\_hint(e) { // var textbox = YAHOO.util.Event.getTarget(e); YAHOO.util.Dom.setStyle('navbar\_password\_hint', "display", "none"); YAHOO.util.Dom.setStyle('navbar\_password', "display", "inline"); YAHOO.util.Dom.get('navbar\_password').focus(); } function navbar\_password(e) { // var textbox = YAHOO.util.Event.getTarget(e); if (textbox.value == '') { YAHOO.util.Dom.setStyle('navbar\_password\_hint', "display", "inline"); YAHOO.util.Dom.setStyle('navbar\_password', "display", "none"); } }

* * *

*   [Home](content.php)
*   [Forum](forum.php)

*   [New Posts](search.php?do=getnew&contenttype=vBForum_Post)
*   [FAQ](faq.php)
*   [Calendar](calendar.php)
*   [Forum Actions](javascript://)
    *   [Mark Forums Read](forumdisplay.php?do=markread&markreadhash=guest)
*   [Quick Links](javascript://)
    *   [Today's Posts](search.php?do=getdaily&contenttype=vBForum_Post)
    *   [View Site Leaders](showgroups.php)

*   [FAQ](faq.php)
*   [Links](local_links.php)
*   [What's New?](search.php?do=getnew&contenttype=vBForum_Post)

   

*   [Advanced Search](search.php)

*   [![Home](images/misc/navbit-home.png "Home")](index.php)
*   [Forum](forum.php)
*   [Qt](forums/1-Qt)
*   [Qt Programming](forums/2-Qt-Programming)
*   Qt displays large size jpg

* * *

    

1.  If this is your first visit, be sure to check out the [**FAQ**](faq.php?) by clicking the link above. You may have to [**register**](register.php?) before you can post: click the register link above to proceed. To start viewing messages, select the forum that you want to visit from the selection below.
2.  Welcome to **Qt Centre**.
    
    [Qt Centre](http://www.qtcentre.org) is a community site devoted to programming in C++ using the [Qt framework](http://qt-project.org). Over 90 percent of questions asked here gets answered. If you are looking for information about Qt related issue — **[register](register.php)** and post your question.
    
    You are currently viewing our boards as a guest which gives you limited access to view most discussions and access our other features. By joining our **free** community you will have access to post topics, communicate privately with other members (PM), respond to polls, upload content and access many other special features. Registration is fast, simple and absolutely free so please, [**join our community today**](http://www.qtcentre.org/register.php)!  
      
    If you have any problems with the registration process or your account login, please [contact us](http://www.qtcentre.org/sendmessage.php).
    

Results 1 to 15 of 15

Thread: [Qt displays large size jpg](threads/30018-Qt-displays-large-size-jpg "Reload this Page")
=================================================================================================

*   ###### [Thread Tools](javascript://)
    
    *   [Show Printable Version](printthread.php?t=30018&pp=20&page=1)
    
*   ###### [Search Thread](javascript://)
    
    *    
    *   [Advanced Search](search.php?search_type=1&searchthreadid=30018&contenttype=vBForum_Post)
        
    
         
    
*   ###### [Display](javascript://)
    
    *   Linear Mode
    *   [Switch to Hybrid Mode](threads/30018-Qt-displays-large-size-jpg?mode=hybrid)
    *   [Switch to Threaded Mode](threads/30018-Qt-displays-large-size-jpg?p=140525&mode=threaded#post140525)

1.  20th April 2010, 07:07 [#1](threads/30018-Qt-displays-large-size-jpg?p=140525#post140525)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Qt displays large size jpg
    -----------------------------------------------------------------------
    
    > Dear all,  
    >   
    > I have trouble displaying large size jpg files in my arm board. My program works for png and jpg which size is under 1mb. It will show error "Pixmap is a null pixmap" if the jpg file is over 2mb or above.  
    >   
    > Does anyone know how to display large size jpg in arm board? Here is the method I used....  
    >   
    > QImage image(filePath);  
    > QPixmap pixmap = QPixmap::fromImage(image);  
    > imageLabel->setPixmap(pixmap.scaled(pixmap.size(),Qt::keepAsp ectRatio));  
    >   
    > Regards,  
    > ![](images/smilies/mad.png "Mad")omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140525 "Reply With Quote")
    
    * * *
    

3.  20th April 2010, 09:13 [#2](threads/30018-Qt-displays-large-size-jpg?p=140543#post140543)
    
    [**Luc4**](members/15928-Luc4 "Luc4 is offline")
    
    *   [View Profile](members/15928-Luc4)
    *   [View Forum Posts](search.php?do=finduser&userid=15928&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/15928-Luc4)
    
    ![Luc4 is offline](images/statusicon/user-offline.png "Luc4 is offline") Intermediate user ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Jan 2010
    
    Posts
    
    190
    
    Thanks
    
    18
    
    Thanked 1 Time in 1 Post
    
    Qt products
    
    ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![MacOS X](images/qtcentre/logo16/macosx.png "MacOS X") ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > Have you tried using QImageReader? It is possible, for the supported formats, to load an image in a specified size. This would avoid the loading of the entire image. Something like this:  
    >   
    > 
    > Qt Code:
    > 
    > Switch view
    > 
    > 1.  [QImageReader](http://qt-project.org/doc/qt-4.8/qimagereader.html) imageReader(fileName);
    >     
    > 2.  imageReader.setScaledSize(sizeLoaded);
    >     
    > 3.  [QImage](http://qt-project.org/doc/qt-4.8/qimage.html) loadedImage \= imageReader.read();
    >     
    > 
    > QImageReader imageReader(fileName);
    > imageReader.setScaledSize(sizeLoaded);
    > QImage loadedImage = imageReader.read();
    > 
    > _To copy to clipboard, switch view to plain text mode_ 
    > 
    >   
    > This way you should be able to read larger images and to do it faster.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140543 "Reply With Quote")
    
    * * *
    
4.  The following user says thank you to Luc4 for this useful post:
    ---------------------------------------------------------------
    
    > [JohannesMunk](member.php?u=3010) (21st April 2010)
    
    * * *
    
5.  20th April 2010, 13:18 [#3](threads/30018-Qt-displays-large-size-jpg?p=140597#post140597)
    
    [![wysota's Avatar](image.php?u=11&dateline=1288868141 "wysota's Avatar")](members/11-wysota "wysota is offline")
    
    [**wysota**](members/11-wysota "wysota is offline")
    
    *   [View Profile](members/11-wysota)
    *   [View Forum Posts](search.php?do=finduser&userid=11&contenttype=vBForum_Post&showposts=1)
    *   [Visit Homepage](http://blog.wysota.eu.org)
    *   [View Articles](https://www.qtcentre.org/list/author/11-wysota)
    
    ![wysota is offline](images/statusicon/user-offline.png "wysota is offline") The "Q" ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png)
    
    [![Nokia Certified Qt Developer](http://www.qtcentre.org/images/qtcentre/qt/Nokia_Certified_Qt_Developer_button.png "Nokia Certified Qt Developer")](http://qt.nokia.com/developer/learning/certification)
    
    Join Date
    
    Jan 2006
    
    Location
    
    Warsaw, Poland
    
    Posts
    
    33,364
    
    Thanks
    
    3
    
    Thanked 5,014 Times in 4,792 Posts
    
    Qt products
    
    ![Qt3](images/qtcentre/logo16/qt3.png "Qt3") ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android") ![Maemo/MeeGo](images/qtcentre/logo16/maemo.png "Maemo/MeeGo")
    
    Wiki edits
    
    [10](/wiki/Special:Contributions/wysota "Wiki edits")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > 2MB jpeg file contains about 24MB of image data (typical jpeg compression is about 1:12). Make sure your device is able to handle as much graphics data.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140597 "Reply With Quote")
    
    * * *
    

7.  20th April 2010, 15:26 [#4](threads/30018-Qt-displays-large-size-jpg?p=140617#post140617)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > Hi all,  
    >   
    >   
    > Thanks for your replies and I will try it but before that I still have a few questions..  
    >   
    >   
    > 1\. I put the above codes in my programs and when I dot the ImageReader QT did not show its properties out ...is it normal cos I have already include <QtGui/QImageReader>.  
    >   
    > 2\. imageReader.setScaledSize(sizeLoaded); ==> what value should I put in variable "sizeLoaded" ?  
    >   
    >   
    > Thanks  
    > ![](images/smilies/confused.png "Confused")omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140617 "Reply With Quote")
    
    * * *
    

9.  20th April 2010, 16:05 [#5](threads/30018-Qt-displays-large-size-jpg?p=140622#post140622)
    
    [**Luc4**](members/15928-Luc4 "Luc4 is offline")
    
    *   [View Profile](members/15928-Luc4)
    *   [View Forum Posts](search.php?do=finduser&userid=15928&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/15928-Luc4)
    
    ![Luc4 is offline](images/statusicon/user-offline.png "Luc4 is offline") Intermediate user ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Jan 2010
    
    Posts
    
    190
    
    Thanks
    
    18
    
    Thanked 1 Time in 1 Post
    
    Qt products
    
    ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![MacOS X](images/qtcentre/logo16/macosx.png "MacOS X") ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > 1\. Qt Creator should list the methods I suppose. Does it build?  
    > 2\. sizeLoaded is the size of the image once loaded.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140622 "Reply With Quote")
    
    * * *
    

11.  21st April 2010, 05:29 [#6](threads/30018-Qt-displays-large-size-jpg?p=140702#post140702)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > When I checked Qt documentation, the value of sizeLoaded should be a QSize type. Since I am new in Qt, what possible values for I set for this QSize type? A number of pixel or a number of other measurement?  
    >   
    > Oh, by the way question one is solved. I reload Qt creator and it list the method.  
    >   
    > Regards,  
    > omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140702 "Reply With Quote")
    
    * * *
    

13.  21st April 2010, 05:45 [#7](threads/30018-Qt-displays-large-size-jpg?p=140704#post140704)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > I have tried the program but it gave me nothing on the screen with no error. what happened?  
    >   
    > the codes:  
    >   
    > QImageReader imageReader(filePath);  
    > imageReader.setScaledSize(imageReader.scaledSize() );  
    > QImage image = imageReader.read();  
    > //QImage image(filePath);  
    > QPixmap pixmap = QPixmap::fromImage(image);  
    > //imageLabel->setPixmap(pixmap.scaled(pixmap.size(),Qt::KeepAsp ectRatio));  
    > imageLabel->setPixmap(pixmap);
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140704 "Reply With Quote")
    
    * * *
    

15.  21st April 2010, 07:51 [#8](threads/30018-Qt-displays-large-size-jpg?p=140723#post140723)
    
    [![wysota's Avatar](image.php?u=11&dateline=1288868141 "wysota's Avatar")](members/11-wysota "wysota is offline")
    
    [**wysota**](members/11-wysota "wysota is offline")
    
    *   [View Profile](members/11-wysota)
    *   [View Forum Posts](search.php?do=finduser&userid=11&contenttype=vBForum_Post&showposts=1)
    *   [Visit Homepage](http://blog.wysota.eu.org)
    *   [View Articles](https://www.qtcentre.org/list/author/11-wysota)
    
    ![wysota is offline](images/statusicon/user-offline.png "wysota is offline") The "Q" ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png)
    
    [![Nokia Certified Qt Developer](http://www.qtcentre.org/images/qtcentre/qt/Nokia_Certified_Qt_Developer_button.png "Nokia Certified Qt Developer")](http://qt.nokia.com/developer/learning/certification)
    
    Join Date
    
    Jan 2006
    
    Location
    
    Warsaw, Poland
    
    Posts
    
    33,364
    
    Thanks
    
    3
    
    Thanked 5,014 Times in 4,792 Posts
    
    Qt products
    
    ![Qt3](images/qtcentre/logo16/qt3.png "Qt3") ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android") ![Maemo/MeeGo](images/qtcentre/logo16/maemo.png "Maemo/MeeGo")
    
    Wiki edits
    
    [10](/wiki/Special:Contributions/wysota "Wiki edits")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > I don't think jpeg supports scaled size loading.  
    >   
    > This line doesn't make any sense, though:  
    > 
    > Qt Code:
    > 
    > Switch view
    > 
    > 1.  imageReader.setScaledSize(imageReader.scaledSize() );
    >     
    > 
    > imageReader.setScaledSize(imageReader.scaledSize() );
    > 
    > _To copy to clipboard, switch view to plain text mode_ 
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140723 "Reply With Quote")
    
    * * *
    

17.  21st April 2010, 08:17 [#9](threads/30018-Qt-displays-large-size-jpg?p=140732#post140732)
    
    [**Luc4**](members/15928-Luc4 "Luc4 is offline")
    
    *   [View Profile](members/15928-Luc4)
    *   [View Forum Posts](search.php?do=finduser&userid=15928&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/15928-Luc4)
    
    ![Luc4 is offline](images/statusicon/user-offline.png "Luc4 is offline") Intermediate user ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Jan 2010
    
    Posts
    
    190
    
    Thanks
    
    18
    
    Thanked 1 Time in 1 Post
    
    Qt products
    
    ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![MacOS X](images/qtcentre/logo16/macosx.png "MacOS X") ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > ![Quote](images/misc/quote_icon.png "Quote") Originally Posted by **omegas** [![View Post](images/buttons/viewpost-right.png "View Post")](showthread.php?p=140704#post140704)
    > 
    > I have tried the program but it gave me nothing on the screen with no error. what happened?  
    >   
    > the codes:  
    >   
    > QImageReader imageReader(filePath);  
    > imageReader.setScaledSize(imageReader.scaledSize() );  
    > QImage image = imageReader.read();  
    > //QImage image(filePath);  
    > QPixmap pixmap = QPixmap::fromImage(image);  
    > //imageLabel->setPixmap(pixmap.scaled(pixmap.size(),Qt::KeepAsp ectRatio));  
    > imageLabel->setPixmap(pixmap);
    > 
    > I see that, by default, the method scaledSize() returns a Qsize (-1, -1). Maybe that's the reason why you get nothing on the screen. You have to set it to the size in pixel you want the image to be loaded into memory.  
    >   
    > 
    > ![Quote](images/misc/quote_icon.png "Quote") Originally Posted by **wysota** [![View Post](images/buttons/viewpost-right.png "View Post")](showthread.php?p=140723#post140723)
    > 
    > I don't think jpeg supports scaled size loading.
    > 
    > As far as I can see yes... I create thumbnails using this technique and works greatly! Moreover I can load very large images that were not loaded otherwise.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140732 "Reply With Quote")
    
    * * *
    

19.  21st April 2010, 08:41 [#10](threads/30018-Qt-displays-large-size-jpg?p=140735#post140735)
    
    [![wysota's Avatar](image.php?u=11&dateline=1288868141 "wysota's Avatar")](members/11-wysota "wysota is offline")
    
    [**wysota**](members/11-wysota "wysota is offline")
    
    *   [View Profile](members/11-wysota)
    *   [View Forum Posts](search.php?do=finduser&userid=11&contenttype=vBForum_Post&showposts=1)
    *   [Visit Homepage](http://blog.wysota.eu.org)
    *   [View Articles](https://www.qtcentre.org/list/author/11-wysota)
    
    ![wysota is offline](images/statusicon/user-offline.png "wysota is offline") The "Q" ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_pos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png) ![](images/reputation/reputation_highpos.png)
    
    [![Nokia Certified Qt Developer](http://www.qtcentre.org/images/qtcentre/qt/Nokia_Certified_Qt_Developer_button.png "Nokia Certified Qt Developer")](http://qt.nokia.com/developer/learning/certification)
    
    Join Date
    
    Jan 2006
    
    Location
    
    Warsaw, Poland
    
    Posts
    
    33,364
    
    Thanks
    
    3
    
    Thanked 5,014 Times in 4,792 Posts
    
    Qt products
    
    ![Qt3](images/qtcentre/logo16/qt3.png "Qt3") ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android") ![Maemo/MeeGo](images/qtcentre/logo16/maemo.png "Maemo/MeeGo")
    
    Wiki edits
    
    [10](/wiki/Special:Contributions/wysota "Wiki edits")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > I think you are right:  
    > 
    > Qt Code:
    > 
    > Switch view
    > 
    > 1.  #include <QtGui>
    >     
    > 
    > 3.  int main(int argc, char \*\*argv){
    >     
    > 4.    [QApplication](http://qt-project.org/doc/qt-4.8/qapplication.html) app(argc, argv);
    >     
    > 5.    [QImageReader](http://qt-project.org/doc/qt-4.8/qimagereader.html) reader("img.jpg", "JPEG");
    >     
    > 6.    qDebug() << "QImageIOHandler::Size:" << reader.supportsOption([QImageIOHandler](http://qt-project.org/doc/qt-4.8/qimageiohandler.html)::Size);
    >     
    > 7.    qDebug() << "QImageIOHandler::ScaledSize:" << reader.supportsOption([QImageIOHandler](http://qt-project.org/doc/qt-4.8/qimageiohandler.html)::ScaledSize);
    >     
    > 8.  }
    >     
    > 
    > #include <QtGui>
    > 
    > int main(int argc, char \*\*argv){
    >   QApplication app(argc, argv);
    >   QImageReader reader("img.jpg", "JPEG");
    >   qDebug() << "QImageIOHandler::Size:" << reader.supportsOption(QImageIOHandler::Size);
    >   qDebug() << "QImageIOHandler::ScaledSize:" << reader.supportsOption(QImageIOHandler::ScaledSize);
    > }
    > 
    > _To copy to clipboard, switch view to plain text mode_ 
    > 
    > $ ./imr  
    > QImageIOHandler::Size: true  
    > QImageIOHandler::ScaledSize: true
    > 
    > Just note scaled loading would work even if ScaledSize returned false here. Only that the whole image would be loaded first and scaled later.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140735 "Reply With Quote")
    
    * * *
    

21.  21st April 2010, 09:04 [#11](threads/30018-Qt-displays-large-size-jpg?p=140738#post140738)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > ![Quote](images/misc/quote_icon.png "Quote") Originally Posted by **Luc4** [![View Post](images/buttons/viewpost-right.png "View Post")](showthread.php?p=140732#post140732)
    > 
    > I see that, by default, the method scaledSize() returns a Qsize (-1, -1). Maybe that's the reason why you get nothing on the screen. You have to set it to the size in pixel you want the image to be loaded into memory.  
    >   
    >   
    >   
    > As far as I can see yes... I create thumbnails using this technique and works greatly! Moreover I can load very large images that were not loaded otherwise.
    > 
    >   
    > Dear Luc4,  
    >   
    > Could you give me a more specific example how to use setScaledSize function since I am a little bit puzzled by it?  
    >   
    > omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140738 "Reply With Quote")
    
    * * *
    

23.  21st April 2010, 09:19 [#12](threads/30018-Qt-displays-large-size-jpg?p=140740#post140740)
    
    [**Luc4**](members/15928-Luc4 "Luc4 is offline")
    
    *   [View Profile](members/15928-Luc4)
    *   [View Forum Posts](search.php?do=finduser&userid=15928&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/15928-Luc4)
    
    ![Luc4 is offline](images/statusicon/user-offline.png "Luc4 is offline") Intermediate user ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Jan 2010
    
    Posts
    
    190
    
    Thanks
    
    18
    
    Thanked 1 Time in 1 Post
    
    Qt products
    
    ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![MacOS X](images/qtcentre/logo16/macosx.png "MacOS X") ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > Well... You can choose whatever size you want I suppose. That's up to you... Let's say you have a very large image, 10000x10000. It's possible an embedded device is unable to load it. So, assuming the format is supported, you can load it in memory in a scaled size, so that you have, let's say, 2000x2000 pixels. So:  
    >   
    > 
    > Qt Code:
    > 
    > Switch view
    > 
    > 1.  [QImageReader](http://qt-project.org/doc/qt-4.8/qimagereader.html) imageReader(fileName);
    >     
    > 2.  imageReader.setScaledSize([QSize](http://qt-project.org/doc/qt-4.8/qsize.html)(2000, 2000));
    >     
    > 3.  [QImage](http://qt-project.org/doc/qt-4.8/qimage.html) imageInMemory \= imageReader.read();
    >     
    > 
    > QImageReader imageReader(fileName);
    > imageReader.setScaledSize(QSize(2000, 2000));
    > QImage imageInMemory = imageReader.read();
    > 
    > _To copy to clipboard, switch view to plain text mode_ 
    > 
    >   
    > This will load into memory 2000x2000 pixels, and it never needs to load entirely the 10000x10000 pixels. Very useful in case you have not enough memory to do so. According to the documentation, the scaling is performed using the scale() method of QImage and the SmoothScaling algorithm. imageInMemory will be a 2000x2000. Information is clearly lost.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140740 "Reply With Quote")
    
    * * *
    

25.  21st April 2010, 09:28 [#13](threads/30018-Qt-displays-large-size-jpg?p=140741#post140741)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > Thanks Luc4... I will try that ....by the way Do u have any experiences on developing arm linux app. for displaying large size image? If so, what is the best Qsize() of pixel for arm app.? I am currently using s3c2440 arm board and I just tried the program but it gave me segmentation fault....maybe it is not the setting or program problem and it may be the problem of my cross compiler since I am using version 4.3.2 EABI one. According to my people comments, if u use this compiler it will always give u segmentation fault error but 4.1.2 is ok...I think I will change it later. Still , please provide any valuable info. from the above...  
    >   
    > Regards,  
    > omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140741 "Reply With Quote")
    
    * * *
    

27.  21st April 2010, 11:51 [#14](threads/30018-Qt-displays-large-size-jpg?p=140758#post140758)
    
    [**Luc4**](members/15928-Luc4 "Luc4 is offline")
    
    *   [View Profile](members/15928-Luc4)
    *   [View Forum Posts](search.php?do=finduser&userid=15928&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/15928-Luc4)
    
    ![Luc4 is offline](images/statusicon/user-offline.png "Luc4 is offline") Intermediate user ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Jan 2010
    
    Posts
    
    190
    
    Thanks
    
    18
    
    Thanked 1 Time in 1 Post
    
    Qt products
    
    ![Qt4](images/qtcentre/logo16/qt4.png "Qt4") ![Qt5](images/qtcentre/logo16/qt4.png "Qt5") ![Qt/Embedded](images/qtcentre/logo16/qpe.png "Qt/Embedded")
    
    Platforms
    
    ![MacOS X](images/qtcentre/logo16/macosx.png "MacOS X") ![Unix/X11](images/qtcentre/logo16/x11.png "Unix/X11") ![Windows](images/qtcentre/logo16/windows.png "Windows") ![Android](images/qtcentre/logo16/android.png "Android")
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > I suppose the choice of the size is more something related to the amount of memory and to the application you're developing. The more pixels you use, the more memory you'll use and the more time will be needed to load large images. What you could do is to load images up to a max size, and then reload only a specific rect in case zooming is required.  
    > I've never experience any segfaults however.
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140758 "Reply With Quote")
    
    * * *
    

29.  22nd April 2010, 05:07 [#15](threads/30018-Qt-displays-large-size-jpg?p=140843#post140843)
    
    [**omegas**](members/17693-omegas "omegas is offline")
    
    *   [View Profile](members/17693-omegas)
    *   [View Forum Posts](search.php?do=finduser&userid=17693&contenttype=vBForum_Post&showposts=1)
    *   [View Articles](https://www.qtcentre.org/list/author/17693-omegas)
    
    ![omegas is offline](images/statusicon/user-offline.png "omegas is offline") Beginner ![](images/reputation/reputation_pos.png)
    
    Join Date
    
    Apr 2010
    
    Posts
    
    9
    
    ![Default](images/icons/icon1.png "Default") Re: Qt displays large size jpg
    ---------------------------------------------------------------------------
    
    > Hi again,  
    >   
    >   
    > It works now. As you mentioned above it may be the cause of memory loaded and after I choose to load the image size by 1/10 or above of it, the images showed up. i.e. imagereader.setScaledSize(imagereader.scaledsize/10).  
    >   
    >   
    > Thanks for all your valuable assistants.  
    >   
    > Cheers,  
    > omegas
    
      ![](images/misc/progress.gif) [![Reply With Quote](clear.gif "Reply With Quote") Reply With Quote](newreply.php?do=newreply&p=140843 "Reply With Quote")
    
    * * *
    

Quick Navigation [Qt Programming](threads/30018-Qt-displays-large-size-jpg) [Top](threads/30018-Qt-displays-large-size-jpg#top)

*   Site Areas
*   [Settings](usercp.php)
*   [Private Messages](private.php)
*   [Subscriptions](subscription.php)
*   [Who's Online](online.php)
*   [Search Forums](search.php)
*   [Forums Home](forum.php)
*   Forums
*   [Qt](forums/1-Qt)
    1.  [Newbie](forums/4-Newbie)
    2.  [Qt Programming](forums/2-Qt-Programming)
        1.  [Qwt](forums/23-Qwt)
    3.  [Qt Quick](forums/42-Qt-Quick)
    4.  [Qt Tools](forums/3-Qt-Tools)
    5.  [Qt-based Software](forums/16-Qt-based-Software)
    6.  [Qt for Embedded and Mobile](forums/14-Qt-for-Embedded-and-Mobile)
    7.  [Installation and Deployment](forums/5-Installation-and-Deployment)
    8.  [KDE Forum](forums/7-KDE-Forum)
*   [Other](forums/8-Other)
    1.  [General Programming](forums/9-General-Programming)
    2.  [ICSNetwork](forums/25-ICSNetwork)
        1.  [Introduction to Qt](forums/26-Introduction-to-Qt)
        2.  [An Introduction to QThreads](forums/30-An-Introduction-to-QThreads)
        3.  [The GraphicsView Framework](forums/31-The-GraphicsView-Framework)
        4.  [What's New in Qt 4.4](forums/32-What-s-New-in-Qt-4-4)
        5.  [Design Patterns in Qt](forums/33-Design-Patterns-in-Qt)
        6.  [The Model-View Framework](forums/34-The-Model-View-Framework)
        7.  [Best Practices in Qt Programming](forums/35-Best-Practices-in-Qt-Programming)
        8.  [Qt Webkit](forums/36-Qt-Webkit)
        9.  [Best Practices for Qt Localization](forums/37-Best-Practices-for-Qt-Localization)
        10.  [What's New in Qt 4.5](forums/38-What-s-New-in-Qt-4-5)
        11.  [This Week in Qt](forums/40-This-Week-in-Qt)
    3.  [General Discussion](forums/10-General-Discussion)
    4.  [Jobs](forums/12-Jobs)
        1.  [Resumes](forums/17-Resumes)

**«** [Previous Thread](threads/30018-Qt-displays-large-size-jpg?goto=nextoldest) | [Next Thread](threads/30018-Qt-displays-large-size-jpg?goto=nextnewest) **»**

#### Similar Threads

1.  ###### [QTableView and changing how a cell displays its contents](threads/24616-QTableView-and-changing-how-a-cell-displays-its-contents "Hi, anyone worked with Oracle databases or binary database datatypes? 
    Im implementing a QTableview with a QSqlQueryModel which can potentially...")
    
    By BitRogue in forum Qt Programming
    
    Replies: 2
    
    Last Post: 9th October 2009, 10:18
    
2.  ###### [Multiple displays on X11](threads/24257-Multiple-displays-on-X11 "I have a graphics card driving 4 seperate display outputs. I am running XServer and trying yo to use these seperate displays.  
    On XServer, each...")
    
    By alisami in forum Qt Programming
    
    Replies: 1
    
    Last Post: 25th September 2009, 17:25
    
3.  ###### [QMenu always displays icons aty 16x16 px](threads/21187-QMenu-always-displays-icons-aty-16x16-px "Hi - I am using QMenu, and I am using a large font in the menu.  I am providing 24x24 pixel icons to the QMenu when I add actions to it, but when the...")
    
    By ghassett in forum Qt Programming
    
    Replies: 3
    
    Last Post: 21st May 2009, 18:41
    
4.  ###### [Sending large datagrams(very large)](threads/11829-Sending-large-datagrams(very-large) "OK you network thumpers, I have some kind of a problem. 
    Is it possible to send large UDP datagrams? 32-33k in my case, Windows client to Windows...")
    
    By marcel in forum General Programming
    
    Replies: 1
    
    Last Post: 16th February 2008, 21:55
    
5.  ###### [QLabel, large, rich text, font size](threads/5508-QLabel-large-rich-text-font-size "Hello.... 
    Really simple one ... (sorry for asking really) 
    How do I get REALLY BIG text into a QLabel? 
    I'm using, 
    QString richText...")
    
    By TheKedge in forum Qt Programming
    
    Replies: 3
    
    Last Post: 5th February 2007, 11:56
    

#### Bookmarks

##### Bookmarks

*   [![Submit to Digg](images/misc/bookmarksite_digg.gif "Submit to Digg")](http://digg.com/submit?phrase=2&url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg) [Digg](http://digg.com/submit?phrase=2&url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg)
*   [![Submit to del.icio.us](images/misc/bookmarksite_delicious.gif "Submit to del.icio.us")](http://del.icio.us/post?url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg) [del.icio.us](http://del.icio.us/post?url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg)
*   [![Submit to StumbleUpon](images/misc/bookmarksite_stumbleupon.gif "Submit to StumbleUpon")](http://www.stumbleupon.com/submit?url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg) [StumbleUpon](http://www.stumbleupon.com/submit?url=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg)
*   [![Submit to Google](images/misc/bookmarksite_google.gif "Submit to Google")](http://www.google.com/bookmarks/mark?op=edit&output=popup&bkmk=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg) [Google](http://www.google.com/bookmarks/mark?op=edit&output=popup&bkmk=https%3A%2F%2Fwww.qtcentre.org%2Fshowthread.php%3Ft%3D30018&title=Qt+displays+large+size+jpg)

#### [![](images/buttons/collapse_40b.png)](threads/30018-Qt-displays-large-size-jpg#top) Posting Permissions

*   You **may not** post new threads
*   You **may not** post replies
*   You **may not** post attachments
*   You **may not** edit your posts

*   [BB code](misc.php?do=bbcode) is **On**
*   [Smilies](misc.php?do=showsmilies) are **On**
*   [\[IMG\]](misc.php?do=bbcode#imgcode) code is **On**
*   [\[VIDEO\]](misc.php?do=bbcode#videocode) code is **On**
*   HTML code is **Off**

[Forum Rules](misc.php?do=showrules)

*   [Contact Us](sendmessage.php)
*   [Qt Centre](https://www.qtcentre.org)
*   [Archive](archive/index.php)
*   [Top](threads/30018-Qt-displays-large-size-jpg#top)

<!-- // Main vBulletin Javascript Initialization vBulletin\_init(); //-->

All times are GMT +1. The time now is 14:27.

Powered by vBulletin Version 4.2.5 Copyright ©2000 - 2021, Jelsoft Enterprises Ltd.,

© 2006–2017 [Qt Centre - The Ultimate Qt Community site](//www.qtcentre.org)

Digia, Qt and their respective logos are trademarks of Digia Plc in Finland and/or other countries worldwide.