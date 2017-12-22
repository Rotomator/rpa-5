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

我们继续录制，先打开TIM，我们录制登录过程。选择Type

![](/assets1.1/import7.png)

使用光标点击账号的输入框。

![](/assets1.1/import8.png)

可以输入账号信息,并勾选“Empty”，在输入之前会首先删除已有的账号信息。确认后点击回车。再次使用同样的方法选择密码框。

![](/assets1.1/import9.png)

点击回车，接下来，点击登录按钮。

![](/assets1.1/import10.png)

选择click，在登录框中点击登录按钮。此时我们就录制完成了登录的部分。你可以点击Save&exit。

![](/assets1.1/import11.png)

对工程进行修改:

1. 在Main工程中找到刚刚密码框，它需要你输入密码。例如，输入"123456"。
2. 启动应用后，我们需要拿到TIM窗口，![](/assets1.1/import12.png)设置选择器的值，为"&lt;wnd app='tim.exe' cls='TXGuiFoundation' title='TIM' /&gt;"
3. 由于TIM程序会在窗口打开时，对光标进行初始化，建议等待1秒后再继续。

![](/assets1.1/import13.png)

保存，然后在UiPath中点击Run,来执行刚刚录制的脚本。

PS. 执行之前别忘记登出刚刚的录入时使用的账号。

已经大功告成了把，我们搜索好友，然后发送消息吧。

![](/assets1.1/import14.png)

首先找到窗口，点击type，

![](/assets1.1/import15.png)

点击搜索栏。输入好友账号。

![](/assets1.1/import16.png)

在搜搜结果中点击第一条，打开聊天窗口

![](/assets1.1/import17.png)

在聊天窗口中输入文字，并点击发送按钮。

![](/assets1.1/import18.png)

save&exit。所有的事情都完成了。点击Run就可以继续了。



