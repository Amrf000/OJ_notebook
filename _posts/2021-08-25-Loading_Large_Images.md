---
layout: post
title: 加载大图像
category: qt
tags: [qt]
---

加载大图像(https://wiki.qt.io/Loading_Large_Images)
=====

来自 Qt 维基

跳转到： [导航](#mw-head)、 [搜索](#p-search)

加载图形时，输入文件有时会比需要的大。幸运的是，Qt 图像加载基础架构考虑到了这一点。在我们了解如何使用它之前，我们先离题并了解一下使用 Qt 加载图像时所涉及的机制。

内容
--

*   [1 加载图像的背景](#Background_to_Loading_Images)
*   [2 使用 QImageReader](#Using_QImageReader)
*   [3 确保支持](#Ensuring_Support)
*   [4 更多信息](#More_Information)

加载图像的背景
-------

每次编写 QPixmap("picture.png") 或 QImage("picture.jpeg") 时，都会要求 Qt 从磁盘加载图像。Qt 支持多种图像格式，在配置 Qt 时可以启用或禁用这些格式。您还可以使用自己的加载（和保存）类为自己的文件格式扩展 Qt。由于这些功能是作为插件实现的，因此您无需重新构建或配置 Qt 即可添加它们。

文件格式由 QImageReader 和 QImageWriter 类处理。反过来，它们依赖 QImageIOPlugin 类，该类充当从 QImageIOHandler 派生的类的工厂。每个图像 i/o 处理程序都可以支持许多功能。标志 ImageOptions 枚举可用选项。充分利用这些功能，您可以提高应用程序可以处理的图像文件的性能和大小。

使用 QImageReader
---------------

控制图像加载的第一步是避免使用 QImage::load 或 QPixmap::load。相反，您需要直接调用 QImageReader 类。这使您可以更直接地控制过程，从而可以微调所使用的设置。

创建和使用图像阅读器基本上就像使用上述方法加载图像一样简单。默认情况下，图像阅读器会自动尝试识别图像格式并处理查找正确 QImageIOHandler 对象所涉及的详细信息。

`QImageReader reader("large.jpeg");`

如果想直接控制文件格式，可以使用 QImageReader::setFormat 函数。另一个有用的格式检测标志是decideFormatFromContents 属性。通过设置这个标志，所有的图像阅读器插件都会被加载，图像数据的实际内容被用来确定文件格式（而不是仅仅查看文件扩展名）。如果图像数据是通过套接字收集的或从数据库 BLOB 中检索的，这会很有用。

为正确的数据源和格式设置阅读器后，您可以查询它的一些基本信息。例如，查看图像的大小。图像 i/o 处理程序可以在不加载完整图像的情况下执行此操作。然而，他们并不是被迫的。您可以在下面的“_确保支持”_部分阅读更多相关信息。

`qDebug() << "Image size:" << reader.size();`

加载大文件时的问题通常是我们不能或不想将整个图像一次保存在内存中。使用 QImageReader::setClipRect 函数，您可以在加载图像时对其进行剪辑。这可用于加载给定图像的有趣部分，或分块加载图像。

`reader.setClipRect(myRect); QImage image = reader.read();`

在场景中仅加载图像的一部分。另一个常见功能是显示图像的较小版本。加载一个非常大的图像，然后将其缩小到合适的大小可能是一个非常消耗内存的操作。同样，这可以使用适当的 QImageReader 函数来解决。通过调用 QImageReader::setScaledSize 函数，您可以设置您希望生成的图像的大小。这让图像 i/o 处理程序在一次操作中加载和缩放图像，将所需的内存减少到最低限度。

`reader.setScaledSize(mySize); QImage image = reader.read();`

请注意，此缩放操作不支持 Qt::AspectRatioMode 标志。相反，您必须采取必要的步骤来自己处理缩放结果的纵横比。

要裁剪和缩放图像，您可以设置 scaledClipRect 属性，该属性在缩放后裁剪图像。

确保支持
----

在纸面上，使用上述任何功能都可以提高图像读取的性能，并减少所需的内存。这在资源有限的嵌入式设置中非常重要，但也应考虑到桌面操作。减少内存需求使缓存运行更高效，并避免了为了交换而启动硬盘驱动器，因此编写高效的代码可以提高性能和电池时间 - 快乐的用户会给快乐的开发人员。

但是，所描述的操作可以由图像 i/o 处理程序或 QImageReader 处理。后者使用简单的实现，即加载完整图像，然后对其进行剪辑和缩放。这不会以任何方式改进您的应用程序。那么，如何确定图像 i/o 处理程序的作用以及 QImageReader 的作用？输入 QImageIOHandler::ImageOptions 标志。

通过使用 QImageReader::supportsOption 函数查询 QImageReader 的特定选项，您可以了解支持什么和不支持什么。在上面的示例中，我们使用了以下功能：

*   QImageIOHandler::Size，图像输入/输出处理程序可以从图像元数据中读取图像的大小。这意味着查询图像大小不会加载完整图像，只会加载所需的标题数据。

*   QImageIOHandler::ClipRect，图像输入/输出处理程序支持在一次操作中剪切和加载图像，潜在地减少内存影响并提高性能

*   QImageIOHandler::ScaledSize，图像 i/o 处理程序支持在一个操作中加载和缩放图像，潜在地减少内存影响并提高性能

*   QImageIOHandler::ScaledClipRect，图像输入/输出处理程序支持在一个操作中加载、缩放和裁剪，潜在地减少内存占用并提高性能

更多信息
----

QImageReader 类提供有关图像的更多信息，而不仅仅是制作图像的像素。可以检索元数据、图像格式的子类型、对增量读取的支持等信息。例如，QImageReader::text 函数返回一个包含图像元数据的 QString，如果图像 i/o 处理程序和图像文件格式支持它。请注意，这个字符串可以被编码来保存数据的键值对，所以它可能需要解析。

这篇文章根本没有涉及的是 QImageWriter，它为写入图像提供了相同级别的控制。使用它，您可以在将图像数据写入文件时调整压缩比、质量设置、字节序等设置。它还可以用于将图像数据写入其他设备，例如套接字和数据库 BLOB。

取自“ [https://wiki.qt.io/index.php?title=Loading\_Large\_Images&oldid=17682](https://wiki.qt.io/index.php?title=Loading_Large_Images&oldid=17682) ”

导航菜单
----

### 个人工具

*   [登入](/index.php?title=Special:QtLogin&returnto=Loading+Large+Images "我们鼓励您登录； 但是，这不是强制性的 [alt-shift-o]")

### 命名空间

*   [页](/Loading_Large_Images "查看内容页面 [alt-shift-c]")
*   [讨论](/index.php?title=Talk:Loading_Large_Images&action=edit&redlink=1 "关于内容页的讨论 [alt-shift-t]")

### 变体[](#)

### 观看次数

*   [读](/Loading_Large_Images)
*   [查看源代码](/index.php?title=Loading_Large_Images&action=edit "此页面受保护。 你可以查看它的源码 [alt-shift-e]")
*   [查看历史记录](/index.php?title=Loading_Large_Images&action=history "此页面的过去修订版 [alt-shift-h]")

### 更多的[](#)

### 搜索

[](/Main "访问主页面")

### 导航

*   [主页](/Main "访问主页 [alt-shift-z]")
*   [近期变动](/Special:RecentChanges "wiki 中的最近更改列表 [alt-shift-r]")
*   [随机页面](/Special:Random "加载一个随机页面 [alt-shift-x]")
*   [关于 MediaWiki 的帮助](https://www.mediawiki.org/wiki/Special:MyLanguage/Help:Contents)

### 工具

*   [这里有什么链接](/Special:WhatLinksHere/Loading_Large_Images "链接到此处的所有 wiki 页面的列表 [alt-shift-j]")
*   [相关变化](/Special:RecentChangesLinked/Loading_Large_Images "从此页面链接的页面的最近更改 [alt-shift-k]")
*   [特殊页面](/Special:SpecialPages "所有特殊页面的列表 [alt-shift-q]")
*   [可打印的版本](/index.php?title=Loading_Large_Images&printable=yes "此页面的可打印版本 [alt-shift-p]")
*   [永久链接](/index.php?title=Loading_Large_Images&oldid=17682 "指向此页面修订版的永久链接")
*   [页面信息](/index.php?title=Loading_Large_Images&action=info "有关此页面的更多信息")

*   此页面的最后编辑时间为 2015 年 6 月 1 日 08:08。

*   [隐私政策](/Qt_Wiki:Privacy_policy "Qt Wiki:隐私政策")
*   [关于 Qt 维基](/Qt_Wiki:About "Qt Wiki:关于")
*   [免责声明](/Qt_Wiki:General_disclaimer "Qt Wiki:一般免责声明")

*   [![由 MediaWiki 提供支持](/resources/assets/poweredby_mediawiki_88x31.png)](//www.mediawiki.org/)

(window.RLQ=window.RLQ||\[\]).push(function(){mw.config.set({"wgPageParseReport":{"limitreport":{"cputime":"0.004","walltime":"0.011","ppvisitednodes":{"value":15,"limit":1000000},"ppgeneratednodes":{"value":20,"limit":1000000},"postexpandincludesize":{"value":0,"limit":2097152},"templateargumentsize":{"value":0,"limit":2097152},"expansiondepth":{"value":2,"limit":40},"expensivefunctioncount":{"value":0,"limit":100},"unstrip-depth":{"value":0,"limit":20},"unstrip-size":{"value":0,"limit":5000000},"timingprofile":\["100.00% 0.000 1 -total"\]},"cachereport":{"timestamp":"20210824234755","ttl":86400,"transientcontent":false}}});}); (function(i,s,o,g,r,a,m){i\['GoogleAnalyticsObject'\]=r;i\[r\]=i\[r\]||function(){ (i\[r\].q=i\[r\].q||\[\]).push(arguments)},i\[r\].l=1\*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)\[0\];a.async=1;a.src=g;m.parentNode.insertBefore(a,m) })(window,document,'script','//www.google-analytics.com/analytics.js','ga'); ga('create', 'UA-54043535-2', 'auto'); ga('set', 'anonymizeIp', true); ga('send', 'pageview'); (window.RLQ=window.RLQ||\[\]).push(function(){mw.config.set({"wgBackendResponseTime":66});});

![Google 翻译](https://www.gstatic.com/images/branding/product/1x/translate_24dp.png)

原文
==

提供更好的翻译建议

* * *