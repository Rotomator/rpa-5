# UI 组件-输入

UiPath提供了各种各样的工具来模拟人类可以做出的所有动作。在自动化流程中输入组件是非常重要的组成部分，常见的输入组件有：点击、输入、快捷键等。

## 输入方法

* 默认\(Default\) - 使用鼠标或者键盘驱动来模拟人类操作\(硬件事件\)，但是这种方法也会有一些不足，例如速度和应用是活动的。
* 模拟输入/点击\(Simulate Type/Click\) - 这种方式速度比较快，由于是在后台运行的，但是它不支持快捷键。 常用在模拟点击或输入。 
* Window消息\(Window Messages\) - 将所有的文本转化为小写,它不能在输入之前清空文本，它的处理速度不是特点快。 它发送特定的消息到目标应用来执行相关action。

下表对这三中输入方法进行的罗列和比对。

|  | 兼容性 | 后台运行 | 速度 | 支持热键 | 自动清空字段 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 默认 | 100% | 否 | 50% | 支持 | 无 |
| Window消息 | 80% | 是 | 50% | 支持 | 无 |
| 模拟输入/点击 | 70% | 是 | 100% | 不支持 | 是 |

## 公共属性

UI输入组件中有很多公共的属性：

* ContinueOnError - 如果找不到组件，流程继续执行。
* DelayAfter – 在动作执行之后暂停时间（毫秒）
* DelayBefore - 在动作开始之前暂停\(毫秒\)
* TimeoutMS \(Milliseconds\) – 查找组件的超时时间。
* WaitForReady – 是否等待整个页面导入
* Target – 目标元素

## UI组件的生命周期

![](/assets2.6/impor1t.png)

1. DelayBefore：在执行之前等待
2. TimeoutMS： 查找元素，
3. 如果超时，根据ContinueOnError确定是否抛出异常
4. 规定时间内找到元素。
5. 执行DelayAfter


