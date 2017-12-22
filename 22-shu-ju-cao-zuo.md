# 2.2 数据操作

流程中里都是数据在流转，本节让我们关注一下数据的操作吧。其实上一节已经对一些数据类型进行了简单的介绍。

## 字符串 Text

文本就是一段文字，例如:  
String itemId = “ASD123”  
String filePath=”Downloads/{0}/output.txt”  
String random=” ASD “

那么在UiPath里常见的字符串操作有哪些呢？

| 方法 | 用法 | 返回值 |
| :--- | :--- | :--- |
| Format | String.Format\(filePath,itemId\) | Downloads/ASD123/output.txt |
| Substring | filePath.Substring\(10\) | ASD123/output.txt |
| Split | filePath.Split\(“/”.ToCharArray\) | Downloads, ASD123, output.txt |
| toLower/toUpper | filePath.ToUpper | DOWNLOADS/ASD123/OUTPUT.TXT |
| Contains | filePath.Contains\(“.”\) | true |
| endsWith/startsWith | filePath.EndsWith\(“.txt”\) | true |
| Replace | filePath.Replace\(“/”,”\”\) | Downloads\ASD123\output.txt |
| Trim | random.Trim | “ASD” |

## 一般类型 Generic Value

该类型为UiPath特有类型,可以代表字符串、数字、日期等等。它使得在流程中处理数据更得心应手。默认的，在UiPath中系统生成的变量都会采用Generic Value。  
如果需要把Generic Value转换到其他类型，可以使用“Assign”。

## 数值 Number

用来保存数值或者数字。数值的格式化：

![](/assets2.2/import1.png)


## List和Array
都是用来保存一个数据集合。和大家熟悉的是类型一样。

## 循环

虚幻在上一节已经说明。除了foreach，还有getrowitem，可以用来获取datatable的数据行。

## 创建DataTable

可以使用buildDataTable来创建数据表。



