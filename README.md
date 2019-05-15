**1.Python中pass语句的作用是什么？**

pass语句什么也不做，一般作为占位符或者创建占位程序，pass语句不会执行任何操作。

**2.Python是如何进行类型转换的？**

Python提供了将变量或值从一种类型转换成另一种类型的内置函数。比如int函数能够将符合数学格式数字型字符串转换成整数。否则，返回错误信息。

**3.Python是如何进行内存管理的？**

Python引用了一个内存池(memory pool)机制，即Pymalloc机制(malloc:n.分配内存)，用于管理对小块内存的申请和释放。

**4.dict 的 items() 方法与 iteritems() 方法的不同？**

items方法将所有的字典以列表方式返回，其中项在返回时没有特殊的顺序；

iteritems方法有相似的作用，但是返回一个迭代器对象

**5.什么是lambda函数？它有什么好处?**

编程中提到的 lambda 表达式，通常是在需要一个函数，但是又不想费神去命名一个函数的场合下使用，也就是指匿名函数。

Python允许你定义一种单行的小函数。定义lambda函数的形式如下：labmda 参数：表达式lambda函数默认返回表达式的值。你也可以将其赋值给一个变量。lambda函数可以接受任意个参数，包括可选参数，但是表达式只有一个。

**6.说明os,sys模块不同，并列举常用的模块方法？**

**官方解释：**

os： This module provides a portable way of usingoperating system dependent functionality.

翻译：提供一种方便的使用操作系统函数的方法。

sys：This module provides access to some variablesused or maintained by the interpreter and to functions that interact stronglywith the interpreter.

翻译：提供访问由解释器使用或维护的变量和在与解释器交互使用到的函数。

