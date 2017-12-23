#Excel和数据表

Excel是UiPath的最常用的场景。本文将带领大家了了解UiPath对Excel的常用操作。例如如何打开Excel文件,读取单元格或区域，输出数据等等。
Excel/工作薄(Workbooks)是基于Excel文件，能存放各种数据的容器。能够格式化，工作表，布局，合并单元格以及多个数据表等等，其实就是你所理解的Excel。
数据表(Data tables)则是一种简单的电子表格，有一些行和列，表头都是可用可无的。

Excel Application Scope是开始所有Excel世界的大门，它是一个容器，你可以用它执行要处理的excel的文件，所有的Excel的操作都需要在它内部执行。
另外，你电脑上如果没有安装Excel，也是可以使用它来执行，但是需要将它的属性“Visible”设置为false。 
除了它之外，还有很多其他操作excel的组件，例如： Read Range, Write Range, Append Range, Sort Table, Read Cell 和 Write Cell, 而数据表的操作组件有For Each Row, Output Data Table, Get Row Item, Add Data Row 以及 Build Data Table。这些组件件如其名。我们挑选几个重点的来说一说。

我们从一个简单的例子开始。有一个Excel文件，我们需要使用UiPath打开该文件，在UiPath的output中打开出其内容,最后将其保存到新文件中。





