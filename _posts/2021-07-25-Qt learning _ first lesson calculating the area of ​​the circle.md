---
layout: post
title: Qt learning _ first lesson calculating the area of ​​the circle
category: qt5
tags: [qt5]
---

```C
double r = 0, s = 0;
QString strr, strs;
strr = ui->lineEdit->text();
r = strr.toDouble();
s = r * r * PI;
ui->lineEdit_2->setText(strs.setNum(s));
```
