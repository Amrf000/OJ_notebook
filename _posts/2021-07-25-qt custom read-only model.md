---
layout: post
title: qt custom read-only model
category: qt5
tags: [qt5]
---
# 

## 

* model / view model data with a view separated, that is to say, we can provide a data model for the different views, QListView, QTableView and QTreeView, so we can show all aspects of the data from different perspectives. However, with the changing needs of thousands, Qt several predefined model is far from meeting the need. Therefore, we must also customize the model.  
Similar to the class QAbstractView custom views, QAbstractItemModel flexible enough to provide a custom interface to the model. It supports hierarchical data source, the data can be CRUD operations, but also to support drag and drop. However, sometimes a flexible class often seems too complicated, so, Qt also provides a QAbstarctListModel and QAbstractTableModel two classes to simplify the development of non-hierarchical data model. As the name suggests, these two classes better suited for use in conjunction with lists and tables.  
Before starting a custom model, we first need to think about this question: our data structure suitable for display what view? Is a list, or a table, or a tree? If our data is only used to display a list or a table, then QAbstractListModel or QAbstractTableModel enough, they realize a lot of the default function for us. However, if our data has a hierarchical structure, and this level must be displayed to the user, we can only choose QAbstractItemModel. No matter what the underlying data structure format, it is best to be considered directly adapted to the standard QAbstractItemModel interface, so you can make more easy access to view this model.  
Now, we start customizing a model. This example adapted from "C ++ GUI Programming with Qt4, 2nd Edition". First, describe demand. We want to achieve is a currency exchange rate table, like banking hall on the walls of the kind of electronic bulletin boards. Of course, you can choose QTableWidget. Indeed, the direct use of QTableWidget really easy. However, imagine that contains 100 currency exchange rate table. Obviously, this is a two-dimensional table, and for each currency, you need to give respect to the other 100 kinds of currency exchange rates (we own their own exchange rate also included, but the exchange rate is always 1.0000). Now, according to our design, this table must be 100 x 100 = 10000 data items. We want to reduce storage space, is there a better way? So we think that our data if the data is not directly displayed to the user, but the currency relative to the US dollar, the exchange rate of other currencies can be calculated according to the exchange rate. For example, I stored the yuan against the US dollar, the yen's exchange rate against the dollar, the yuan's exchange rate against the Japanese yen as long as it can get than a. This data structure is no need to store 10,000 data items, as long as the memory 100 is enough (in reality this may be unrealistic because the two operations will bring greater error, but we do not now consider category).  
So we designed a CurrencyModel class. It underlayer using QMap <QString, double\> data structure is stored, QString types of bonds is the currency name, double the value of the currency type is relatively dollar. (Here mention that, in practical application, never use double the amount of processing sensitive data! Because the double is imprecise, but this is clearly not in our consideration.)  
First file from scratch began to read:  
class CurrencyModel : public QAbstractTableModel  
{  
public:  
CurrencyModel(QObject \*parent = 0);  
void setCurrencyMap(const QMap<QString, double\> &map);  
int rowCount(const QModelIndex &parent) const;  
int columnCount(const QModelIndex &parent) const;  
QVariant data(const QModelIndex &index, int role) const;  
QVariant headerData(int section, Qt::Orientation orientation, int role) const;  
private:  
QString currencyAt(int offset) const;  
QMap<QString, double\> currencyMap;  
};  
This code is black and white, we inherited QAbstractTableModel class, then override a few functions required. The same is true constructor:  
CurrencyModel::CurrencyModel(QObject \*parent)  
: QAbstractTableModel(parent)  
{}  
the rowCount () and the columnCount () Returns the number of rows and columns. Remember that we are saved each currency relative to the US dollar, while the exchange rate between the need to show them every two so these two functions should return the number of items in the map:  
int CurrencyModel::rowCount(const QModelIndex & parent) const  
{  
return currencyMap.count();  
}  
int CurrencyModel::columnCount(const QModelIndex & parent) const  
{  
return currencyMap.count();  
}  
headerData () to return the column name:  
QVariant CurrencyModel::headerData(int section, Qt::Orientation, int role) const  
{  
if (role != Qt::DisplayRole) {  
return QVariant();  
}  
return currencyAt(section);  
}  
We introduced the concept of roles in the previous chapters. Here we first determine whether this role is not for display, and if so, call currencyAt () function returns the name of the first section of the column; if not a blank QVariant object is returned. currencyAt () function is defined as follows:  
QString CurrencyModel::currencyAt(int offset) const  
{  
return (currencyMap.begin() + offset).key();  
}  
If you do not understand QVariant class, you can simply think that this type inside the Java equivalent of Object, which provides most of the data type Qt package up, play a role in type erasure. Such as our cell's data can be string, it can be int, and can also be a color value, so much the type of how to use a function to return it? Recall, the return value is not used to distinguish one function. So, Qt provides QVariant type. You can put a lot into the store type, to use when you need to use a series of function can be taken out. For example, the int packed into a QVariant, use the time to use QVariant :: toInt () to re-take it. This is very similar to the union, but the union's problem is not the type to keep no default constructor, so Qt provides QVariant as a simulation of the union.  
setCurrencyMap () function is used to set the actual underlying data. Since we can not hard-coded such data, we must provide a function for setting the model:  
void CurrencyModel::setCurrencyMap(const QMap<QString, double\> &map)  
{  
beginResetModel();  
currencyMap = map;  
endResetModel();  
}  
Of course, we can directly currencyMap, but we still added beginResetModel () and endResetModel () two function calls. This will tell the other class care model, and now you want to reset the internal data, we have to be prepared. This is a contract type of programming.  
Next is the most complex data () function:  
QVariant CurrencyModel::data(const QModelIndex &index, int role) const  
{  
if (!index.isValid()) {  
return QVariant();  
}  
if (role == Qt::TextAlignmentRole) {  
return int(Qt::AlignRight | Qt::AlignVCenter);  
} else if (role == Qt::DisplayRole) {  
QString rowCurrency = currencyAt(index.row());  
QString columnCurrency = currencyAt(index.column());  
if (currencyMap.value(rowCurrency) == 0.0) {  
return "\#\#\#\#";  
}  
double amount = currencyMap.value(columnCurrency)  
/ currencyMap.value(rowCurrency);  
return QString("%1").arg(amount, 0, 'f', 4);  
}  
return QVariant();  
}  
data () function returns a data cell. It has two parameters: the first is QModelIndex, i.e. the position of cells; the second is the role, that is, the character data. The return value of this function is QVariant type. We first determine the incoming index is not legitimate, if not legitimate direct return a blank QVariant. Then if the role is Qt :: TextAlignmentRole, that is, text alignment, return int (Qt :: AlignRight | Qt :: AlignVCenter); if it is Qt :: DisplayRole, will be calculated according to the logic we said earlier, then format string is returned. This time you will find, in fact, not a data we returned in the if ... else ... there type: if there is a return int, but else there is QString, this is the role of the QVariant.  
To look at the actual results, we can use this main () function Code:  
int main(int argc, char \*argv\[\])  
{  
QApplication a(argc, argv);  
QMap<QString, double\> data;  
data\["USD"\] = 1.0000;  
data\["CNY"\] = 0.1628;  
data\["GBP"\] = 1.5361;  
data\["EUR"\] = 1.2992;  
data\["HKD"\] = 0.1289;  
QTableView view;  
CurrencyModel \*model = new CurrencyModel(&view);  
model-\>setCurrencyMap(data);  
view.setModel(model);  
view.resize(400, 300);  
view.show();  
return a.exec();  
}  
This is our actual operating results:  
![](/public/assets/2021-07-25/153d961786e83d528e5c04f0c84c83f6.png)  
Custom Read-only model