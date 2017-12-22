# 2.2 数据操作

流程中里都是数据在流转，本节让我们关注一下数据的操作吧。

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

该类型为UiPath特有类型,可以代表字符串、数字、日期等等。






