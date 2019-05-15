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

**7.Python里面如何拷贝一个对象？deepcopy 和 copy的区别？**

copy 仅拷贝对象本身，而不拷贝对象中引用的其它对象。

deepcopy 除拷贝对象本身，而且拷贝对象中引用的其它对象。

**8.os.path和sys.path的区别？**

os.path是module，包含了各种处理长文件名(路径名)的函数。

sys.path是由目录名构成的列表，Python 从中查找扩展模块( Python 源模块, 编译模块,或者二进制扩展). 启动 Python 时,这个列表从根据内建规则,PYTHONPATH 环境变量的内容, 以及注册表( Windows 系统)等进行初始化.

**9.re模块中match和search方法的不同？**

match() 函数只检查 RE 是否在字符串开始处匹配，而search() 则是扫描整个字符串。

**10.解释生成器(generator)与函数的不同，并实现和使用简单generator？**

生成器和函数的主要区别在于函数 return avalue，生成器 yield a value同时标记或记忆point of the yield 以便于在下次调用时从标记点恢复执行。 yield 使函数转换成生成器，而生成器反过来又返回迭代器。

**11.解释一下 WSGI 和 FastCGI 的关系？**

**CGI**全称是“公共网关接口”(CommonGateway Interface)，HTTP服务器与你的或其它机器上的程序进行“交谈”的一种工具，其程序须运行在网络服务器上。　CGI可以用任何一种语言编写，只要这种语言具有标准输入、输出和环境变量。如php,perl,tcl等。

**FastCGI**像是一个常驻(long-live)型的CGI，它可以一直执行着，只要激活后，不会每次都要花费时间去fork一次(这是CGI最为人诟病的fork-and-execute模式)。它还支持分布式的运算, 即 FastCGI 程序可以在网站服务器以外的主机上执行并且接受来自其它网站服务器来的请求。

**FastCGI**是语言无关的、可伸缩架构的CGI开放扩展，其主要行为是将CGI解释器进程保持在内存中并因此获得较高的性能。众所周知，CGI解释器的反复加载是CGI性能低下的主要原因，如果CGI解释器保持在内存中并接受FastCGI进程管理器调度，则可以提供良好的性能、伸缩性、Fail- Over特性等等。

**WSGI**的全称为： PythonWeb Server Gateway Interface v1.0 （Python Web 服务器网关接口），

它是 Python 应用程序和 WEB 服务器之间的一种接口。

它的作用，类似于FCGI 或 FASTCGI 之类的协议的作用。

WSGI 的目标，是要建立一个简单的普遍适用的服务器与 WEB 框架之间的接口。

**Flup**就是使用 Python 语言对 WSGI 的一种实现，是可以用于 Python 的应用开发中的一种工具或者说是一种库。

Spawn-fcgi是一个小程序，这个程序的作用是管理fast-cgi进程，那么管理wsgi进程也是没有问题的，功能和php-fpm类似。

故，简单地说，WSGI和FastCGI都是一种CGI，用于连接WEB服务器与应用程序，而WSGI专指Python应用程序。而flup是WSGI的一种实现，Spawn-fcgi是用于管理flup进程的一个工具，可以启动多个wsgi进程，并管理它们。

**12.解释一下 Django 和 Tornado 的关系、差别**

**Django**源自一个在线新闻 Web站点，于 2005 年以开源的形式被释放出来。

Django 框架的核心组件有：

用于创建模型的对象关系映射为最终用户设计的完美管理界面一流的 URL 设计设计者友好的模板语言缓存系统等等。它鼓励快速开发,并遵循MVC设计。Django遵守 BSD版权，最新发行版本是Django

1.4，于2012年03月23日发布.Django的主要目的是简便、快速的开发数据库驱动的网站。它强调代码复用,多个组件可以很方便的以“插件”形式服务于整个框架，Django有许多功能强大的第三方插件，你甚至可以很方便的开发出自己的工具包。这使得Django具有很强的可扩展性。它还强调快速开发和DRY(Do Not RepeatYourself)原则。

**Tornado**是 FriendFeed使用的可扩展的非阻塞式 web 服务器及其相关工具的开源版本。这个 Web 框架看起来有些像 web.py 或者 Google 的 webapp，不过为了能有效利用非阻塞式服务器环境，这个 Web 框架还包含了一些相关的有用工具和优化。

Tornado 和现在的主流 Web 服务器框架（包括大多数Python 的框架）有着明显的区别：它是非阻塞式服务器，而且速度相当快。得利于其 非阻塞的方式和对epoll的运用，Tornado 每秒可以处理数以千计的连接，这意味着对于实时 Web服务来说，Tornado 是一个理想的 Web 框架。我们开发这个 Web 服务器的主要目的就是为了处理 FriendFeed 的实时功能 ——在 FriendFeed 的应用里每一个活动用户都会保持着一个服务器连接。（关于如何扩容 服务器，以处理数以千计的客户端的连接的问题。

**13.解释下django-debug-toolbar的使用**

使用django开发站点时，可以使用django-debug-toolbar来进行调试。在settings.py中添加’debug_toolbar.middleware.DebugToolbarMiddleware’到项目的MIDDLEWARE_CLASSES 内。

