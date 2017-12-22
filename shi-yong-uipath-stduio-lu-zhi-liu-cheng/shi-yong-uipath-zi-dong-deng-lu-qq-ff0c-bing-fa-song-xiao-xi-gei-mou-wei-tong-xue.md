# 使用UiPath自动登录QQ，并发送消息给某位同学

整个例子的过程：  
 1. 使用UiPath登陆QQ  
 2. 使用UiPath点击某位好友  
 3. 发送消息给该好友

使用UiPath登陆QQ

首先打开UiPath Studio，点击创建Blank,创建一个空工程。

![](/assets1.1/import1.png)

在弹出的窗口里填入工程名称以及项目位置。

![](/assets1.1/import2.png)

创建完成后，你能看到整个UiPath studio

![](/assets1.1/import3.png)

点击录制按钮，选择desktop

![](/assets1.1/import4.png)

我们首先启动QQ，点击Start App，用鼠标画出要启动的图标。在弹出的框内输入TIM的路径。

![](/assets1.1/import5.png)

点击ok，再次回到录制的界面。点击Save&exit，再次回到UiPath Studio。

![](/assets1.1/import6.png)

在Main工程里已经能看到刚才录制的内容。我们继续录制，先打开TIM，我们录制登录过程。



