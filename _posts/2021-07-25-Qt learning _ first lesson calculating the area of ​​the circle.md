---
layout: post
title: Qt learning _ first lesson calculating the area of ​​the circle
category: qt5
tags: [qt5]
---
1. double r = 0, s = 0;

2. QString strr, strs;

3. strr = ui-\>lineEdit-\>text();

4. r = strr.toDouble();

5. s = r \* r \* PI;

6. ui-\>lineEdit\_2-\>setText(strs.setNum(s));