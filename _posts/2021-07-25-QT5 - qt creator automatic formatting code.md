---
layout: post
title: QT5 - qt creator automatic formatting code
category: qt5
tags: [qt5]
---
VS used are known per writing a code automatically spaces on both sides of each operator and formatting codes, this feature saves time coding, without manual knock box and structured format.

If the cross-platform program to write, using qt creator more appropriate. qt creator can also implement this feature.

------------------------------------------

If qt creator version is greater than 4.8, then congratulations, you only need a simple configuration.

Help -\> About Plug-ins,

![](/md_blog/public/assets/2021-07-25/f254445d4e2c58e13febda0578d3aa07.png)

Restart.

Tools -\> Options,

![](/md_blog/public/assets/2021-07-25/afc97568c0cabaca521a6e8c34c3b58f.png)

![](/md_blog/public/assets/2021-07-25/f5f3a72d99c1792f9427641d516ee059.png) 

If the compiler is MSVC2017, then the location is clang-format.exe position shown in FIG. You can search about everything. If other compiler, with everything found it.

predefined style, format and style of native webkit qt creator is the same, the function name Below are two braces. Other styles are native Java style, the first braces and function names in a row.

Once configured, click "Run" and they will automatically typesetting.

--------------------------------------------------------

If qt creator version is less than 4.8, please refer to this article.

[https://www.vikingsoftware.com/using-clang-format-with-qtcreator/](https://www.vikingsoftware.com/using-clang-format-with-qtcreator/)

His 4.7