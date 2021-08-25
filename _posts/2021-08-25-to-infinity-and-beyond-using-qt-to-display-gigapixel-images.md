---
layout: post
title: To Infinity and Beyond – 使用 Qt 显示十亿像素图像
category: qt
tags: [qt]
---

To Infinity and Beyond – 使用 Qt 显示十亿像素图像(http://georglempe.de/wordpress/index.php/2020/02/to-infinity-and-beyond-using-qt-to-display-gigapixel-images/)
=====

[跳到内容](#site-content)

 [![](/md_blog/public/assets/2021-08-25/cropped-logo-4.png)](http://georglempe.de/wordpress/ "Georg Lempe 工程解决方案")Georg Lempe 工程解决方案

测量、分析、交互

*   [家](http://georglempe.de/)
*   [文件夹](http://georglempe.de/wordpress/index.php/portfolio/)
*   [博客](http://georglempe.de/wordpress/index.php/blog/)
*   [接触](http://georglempe.de/wordpress/index.php/contact/)

[

菜单

](#)

[

关闭

](#)

*   [家](http://georglempe.de/)
    
*   [文件夹](http://georglempe.de/wordpress/index.php/portfolio/)
    
*   [博客](http://georglempe.de/wordpress/index.php/blog/)
    
*   [接触](http://georglempe.de/wordpress/index.php/contact/)
    

© 2021 [Georg Lempe Engineering Solutions](http://georglempe.de/wordpress)

To Infinity and Beyond – 使用 Qt 显示十亿像素图像
=======================================

*   [发布日期 2020 年 2 月 26 日](http://georglempe.de/wordpress/index.php/2020/02/to-infinity-and-beyond-using-qt-to-display-gigapixel-images/)
*   帖子类别 在[Qt的](http://georglempe.de/wordpress/index.php/category/qt/)，[UI](http://georglempe.de/wordpress/index.php/category/ui/)

![](/md_blog/public/assets/2021-08-25/heic0406a.jpg)

图片来源：美国宇航局、欧空局/哈勃

哈勃太空望远镜项目提供了许多迷人的图像，如上图。其中一些具有大分辨率，例如 GOODS South 场上方的这种分辨率，分辨率为 31813 x 19425 像素，大小为 928 MB。  
虽然图像本身值得详细讨论，但在这篇文章中，我想展示一种如何在 Qt / QtQuick 应用程序中处理此类图像的方法。这将作为如何处理由卫星、显微镜等提供的大图像数据的示例。

![](/md_blog/public/assets/2021-08-25/scale_image.gif)

可缩放平铺图像的示例。出于演示目的，单个图块的重新加载通过不透明动画突出显示，使它们在重新加载时闪烁。  

由于整个图像（或可能）太大而无法以全分辨率加载并保存在内存中，因此它被分成更易于管理的大小的图块。这些图块可以以所需的分辨率快速加载和删除，或者在不需要时保持较小的分辨率。以下示例应用程序旨在演示如何在用户缩放和平移时异步组织这些图块。  
示例应用程序的核心是一个实现，[`QAbstractTableModel`](https://doc.qt.io/qt-5/qabstracttablemodel.html)它将图像数据提供为按行和列排列的单个图块。模型内容显示在[`TableView`](https://doc.qt.io/qt-5/qml-qtquick-tableview.html)最近已（重新）添加到 QtQuick的大修中。

我使用[ImageMagick](https://imagemagick.org/)将大图像分割成大小相等的小图块，其中每个图块的行和列位置是文件名的一部分。对于上面的图像，这会生成一个包含 2.000 多个单独图像的文件夹。

    convert heic0602a.jpg -crop 512X512 -set filename:tile "%[fx:page.y/512]_%[fx:page.x/512]" tiles/tile_%[filename:tile].jpg

用于管理这些图块的表模型从目录中读取图块并`ImageTile`为每个条目创建一个。这个`ImageTile`类看起来像这样：

    class ImageTile : public QObject
    {
        Q_OBJECT
        Q_PROPERTY(int row READ getRow CONSTANT)
        Q_PROPERTY(int column READ getColumn CONSTANT)
        Q_PROPERTY(QString fileName READ getFileName CONSTANT)
    
    public:
        explicit ImageTile(int row, int column, QString fileName, QObject *parent = nullptr);
        Q_INVOKABLE int getRow() { return row; }
        Q_INVOKABLE int getColumn() { return column; }
        Q_INVOKABLE QString getFileName() { return fileName; }
        QImage getImage() { return image; }
        void setImage(QImage image);
        void clearImage();
    
    signals:
        void imageChanged();
    
    private:
        QString fileName;
        QImage image;
        QRect window;
        int row{0};
        int column{0};
    };

表模型需要知道哪些图像需要以哪种分辨率加载。因此，它需要知道当前显示图像的哪一部分以及以何种分辨率显示。为了实现这一点，每当图像的可见窗口发生变化时，QtQuick 前端都会通知模型当前的几何形状和比例。

    void ImageTilesModel::setGeometry(QRect visibleWindow, qreal scale)
    {
        qDebug() << Q_FUNC_INFO << visibleWindow << scale;
        this->visibleWindow = visibleWindow;
        this->scale = scale;
        updateTiles();
    }

这将启动更新过程，其中检查每个图块是否在可见窗口内。工作线程中的每个 tile 都会启动，这将在后台加载 tile。工作线程被组织成一个接一个地[`QThreadPool`](https://doc.qt.io/qt-5/qthreadpool.html)照顾或运行它们。

    void ImageTilesModel::updateTiles()
    {
        qDebug() << Q_FUNC_INFO;
        workerPool.clear();
        QSize scaledTileSize = scale * tileSize;
        for(auto&&row: tiles) {
            for(auto&&tile: row) {
                QRect tileRect(tile->getColumn() * tileSize.width(),
                               tile->getRow() * tileSize.height(),
                               tileSize.width(),
                               tileSize.height()
                               );
                if(tileRect.intersects(visibleWindow)) {
                    if(tile->getImage().size().width() < scaledTileSize.width()) {
                        ImageTileWorker* worker = new ImageTileWorker(tile, scaledTileSize);
                        worker->setAutoDelete(true);
                        workerPool.start(worker);
                    }
                }
            }
        }
    }

worker 类本身很小，因为它只有一项工作，即加载图像并将其缩放到所需的大小。

    class ImageTileWorker : public QObject, public QRunnable
    {
        Q_OBJECT
    public:
        explicit ImageTileWorker(ImageTile* tile, QSize requestedSize, QObject *parent = nullptr);
        void run() override;
    
    signals:
    
    private:
        QSize requestedSize;
        ImageTile* tile = nullptr;
    };
    
    void ImageTileWorker::run() {
        qDebug() << Q_FUNC_INFO;
        QImage image(tile->getFileName());
        image = image.scaled(requestedSize.width(), requestedSize.height());
        tile->setImage(image);
    }
    

磁贴通知表格模型，其内容已更改。然后，表模型使用 dataChanged 信号通知 TableView 特定图块已更改。请注意，TableView`contentHeight`和`contentWidth`属性是手动设置的，而不是让 TableView 按照[此处的建议](https://doc.qt.io/qt-5/qml-qtquick-tableview.html#contentHeight-prop)自行解决。  
另请注意，必须通过其隐式属性设置单个单元格的宽度和高度。设置他们明确地会被忽略[记录在这里](https://doc.qt.io/qt-5/qml-qtquick-tableview.html#delegate-prop)。  
委托中的不透明度动画仅用于调试和演示，以便在 tile 发生变化时进行可视化。

    TableView {
                id: table
                property int tileHeight: tilesModel.tileSize.height
                property int tileWidth: tilesModel.tileSize.width
                height: rows * tileHeight
                width: columns * tileWidth
                contentHeight: rows * tileHeight
                contentWidth: columns * tileWidth
                model: tilesModel
                interactive: false
                delegate: Item {
                    //explicit width and height are ignored, see:
                    //https://doc.qt.io/qt-5/qml-qtquick-tableview.html#delegate-prop
                    implicitHeight: table.tileHeight
                    implicitWidth: table.tileWidth
                    Image {
                        id: img
                        anchors.fill: parent
                        source: "image://tileProvider/" + tile.row + "," + tile.column + "," + Math.random()
                        onSourceChanged: PropertyAnimation { target: img; property: "opacity"; from: 0; to: 1}
                    }
                }
            }

这会触发 TableView 中的更新并从自定义 QQuickImageProvider 加载新图像：

    QImage ImageTileProvider::requestImage(const QString &id, QSize *size, const QSize &requestedSize)
    {
        qDebug() << Q_FUNC_INFO << id << size << requestedSize;
        QImage image;
        QStringList positions = id.split(",");
        if(positions.size() < 2)
        {
            qCritical() << "bad image id" << id;
        }
        else
        {
            int row = positions.at(0).toInt();
            int column = positions.at(1).toInt();
            image = model->getImage(row, column);
        }
        size->setWidth(image.width());
        size->setHeight(image.height());
        return image;
    }

暂时就这样了。上面的代码是一个例子和灵感来源。它不应该被误认为是生产就绪，因为几乎没有错误处理。如有任何申请问题或想法，请随时与我联系。完整的代码需要一些修改才能出现在我的 GitHub 帐户上。

帖子导航
----

[←上一篇：使用 Qt 进行光谱传感](http://georglempe.de/wordpress/index.php/2020/01/spectral-sensing-with-qt/)

[→下一篇：在 Blender 中渲染点云](http://georglempe.de/wordpress/index.php/2020/08/rendering-point-clouds-in-blender/)

### 相关文章

[](http://georglempe.de/wordpress/index.php/2020/12/tableview-tutorial-featuring-conways-game-of-life/)

[以康威的生命游戏为特色的 TableView 教程](http://georglempe.de/wordpress/index.php/2020/12/tableview-tutorial-featuring-conways-game-of-life/)
--------------------------------------------------------------------------------------------------------------------------------

*   [发布日期 2020 年 12 月 1 日](http://georglempe.de/wordpress/index.php/2020/12/tableview-tutorial-featuring-conways-game-of-life/)

[](http://georglempe.de/wordpress/index.php/2020/01/spectral-sensing-with-qt/)

[使用 Qt 进行光谱传感](http://georglempe.de/wordpress/index.php/2020/01/spectral-sensing-with-qt/)
------------------------------------------------------------------------------------------

*   [发布日期 2020 年 1 月 7 日](http://georglempe.de/wordpress/index.php/2020/01/spectral-sensing-with-qt/)

[](http://georglempe.de/wordpress/index.php/2020/01/docking-example-using-qtquick/)

[使用 QtQuick 的停靠示例](http://georglempe.de/wordpress/index.php/2020/01/docking-example-using-qtquick/)
---------------------------------------------------------------------------------------------------

*   [发布日期 2020 年 1 月 3 日](http://georglempe.de/wordpress/index.php/2020/01/docking-example-using-qtquick/)

[](http://georglempe.de/wordpress/index.php/2020/08/rendering-point-clouds-in-blender/)

[在 Blender 中渲染点云](http://georglempe.de/wordpress/index.php/2020/08/rendering-point-clouds-in-blender/)
------------------------------------------------------------------------------------------------------

*   [发布日期 2020 年 8 月 7 日](http://georglempe.de/wordpress/index.php/2020/08/rendering-point-clouds-in-blender/)

跟着我
---

*   [链接](https://www.linkedin.com/in/georg-lempe-237bb178/)
*   [兴](https://www.xing.com/profile/Georg_Lempe/cv)
*   [github](https://github.com/wbt729)

© 2021 [Georg Lempe Engineering Solutions](http://georglempe.de/wordpress)

![Google 翻译](https://www.gstatic.com/images/branding/product/1x/translate_24dp.png)

原文
==

提供更好的翻译建议

* * *