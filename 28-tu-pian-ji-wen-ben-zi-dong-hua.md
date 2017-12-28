# Citrix自动化

前几个章节我们介绍了UiPath录制包括基本、Web、应用以及citrix。本节开始我们将介绍citrix。本节将说明虚拟应用自动化以及如何手动的添加组件到流程中。另外也会使用OCR对虚拟主机（Citrix）进行文本输出。

## 虚拟主机

虚拟主机通常运行在服务器端,将界面流传输给用户。

![](/assets2.8/import1.png)

因此，UiPath无法通过基本的录制来操作。因此UiPath专门为citrix提供了录制。

涉及的组件有：

* 点击图片\(Click Image\) - 组件被用来点击图片、按钮、菜单以及其他相关元素。
* 点击文本\(Click Text\) - 它使用OCR来扫描虚拟主机的屏幕，使得你能够获取指定像素的文本，然后对它进行操作。
* 选择&拷贝\(Select & Copy\) - 非常简单的Citrix自动化,但是适合选择文本
* Scrape Relative - 允许你获取image区域的数据。



