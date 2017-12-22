# 使用UiPath获取天气数据，并发送邮件给自己

这个例子中我们将使用UiPath获取Web页面中的数据，并将其使用邮件发送出去。

天气数据我们从 [http://www.weather.com.cn](http://www.weather.com.cn) 中获取吧。在这个例子中我们尝试获取北京7天内的天气数据。

首先打开UiPath Studio，新建一个空白工程。在菜单栏中选择“Data Scrping”。

![](/assets1.1/import20.png)

弹出Data Scraping的对话框

![](/assets1.1/import21.png)

我们需要打开浏览器，输入北京天气地址。 我们找到需要提取的数据。

![](/assets1.1/import22.png)

需要获取数据有这个几个： 日期，天气情况，温度，风力。在Data Scraping的对话框点击下一步，在网页中选择天气，例如22日（今天）

![](/assets1.1/import23.png)

首先UiPath知道我们要选择的内容，接着它需要定义一个模板，因此你需要再提供一个类似的日期比如28日\(周四\)

![](/assets1.1/import24.png)

设置当前字段的列名称。点击下一步，预览吧。

![](/assets1.1/import25.png)

我们还需要其他行，点击“extract Correlated Data”，采用类似的方法把我们关心的其他行都提取出来吧。

![](/assets1.1/import26.png)

点击完成，我们回到UiPath Studio，可以看到创建好的数据，系统默认将这些数据保存到变量ExtractTatatable。

接下来，拖出Write CSV，定义csv的目录和名字。并制定csv的DataTable为ExtractTatatable。写完CSV文件就需要把文件发送出来啦。拖出“Send STMP Mail message”输入邮件具体信息，在附件中添加一个入参，将刚刚保存的csv文件名填入到in的表达式里。

PS. STMP 需要STMP服务器地址以及账号信息。

![](/assets1.1/import27.png)

大家根据自己的情况来填写配置信息吧。

最后到了激动人心的执行时刻了。等待机器人跑完。我们查看邮箱吧。

![](/assets1.1/import28.png)

打开附件

![](/assets1.1/import29.png)

好啦，机器人如果每天早上9点准点给你发邮件，梦寐以求的生活来啦，小秘书登场！！！

