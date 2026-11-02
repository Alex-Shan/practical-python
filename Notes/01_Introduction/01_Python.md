[目录](../Contents.md) \| [下一节（1.2 第一个程序）](02_Hello_world.md)

# 1.1 Python

### 什么是 Python？

Python 是一种解释型高级编程语言，通常被归类为[“脚本语言”](https://en.wikipedia.org/wiki/Scripting_language)，与 Perl、Tcl、Ruby 等语言类似。其语法在一定程度上受到 C 语言元素的启发。

Python 由 Guido van Rossum 于 1990 年前后创建，以 Monty Python 喜剧团体命名。

### 从哪里获取 Python？

可从 [Python.org](https://www.python.org/) 获取 Python。本课程只需要基本安装，建议使用 Python 3.6 或更新版本。讲义和解答使用 Python 3.6。

### 为什么要创建 Python？

用 Python 创始人的话来说：

> 我创建 Python 的最初动机，是感觉 Amoeba [操作系统] 项目需要一种更高级的语言。我意识到，用 C 开发系统管理工具耗时太长。而且，出于多种原因，Bourne shell 也不适合这些任务。……因此，需要一种语言来填补 C 与 shell 之间的空白。
>
> ——Guido van Rossum

### 我的机器上的 Python 在哪里？

虽然 Python 可以在许多环境中运行，但通常作为一个可从终端或命令行 shell 启动的程序安装在机器上。在终端中，应该能这样输入 `python`：

```
bash $ python
Python 3.8.1 (default, Feb 20 2020, 09:29:22)
[Clang 10.0.0 (clang-1000.10.44.4)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello world")
hello world
>>>
```

如果不熟悉 shell 或终端，建议先暂停学习，完成一个简短的相关教程，再回来继续。

虽然许多非 shell 环境也可以编写 Python，但掌握在终端中运行、调试和交互的能力，会让你成为更强的 Python 程序员。这是 Python 的原生环境；能够在这里使用，就能在其他环境中使用。

## 练习

### 练习 1.1：将 Python 用作计算器

在机器上启动 Python，将其用作计算器解决以下问题。

幸运的 Larry 以每股 235.14 美元买入了 75 股 Google 股票。今天股价为 711.25 美元。用 Python 交互模式计算：如果卖出全部股票，他能赚多少？

```python
>>> (711.25 - 235.14) * 75
35708.25
>>>
```

小技巧：下划线（\_）变量保存上一次计算的结果。例如，贪婪的经纪人抽取 20% 后，Larry 还能赚多少？

```python
>>> _ * 0.80
28566.600000000002
>>>
```

### 练习 1.2：获取帮助

使用 `help()` 查看 `abs()` 的帮助，再查看 `round()` 的帮助。直接输入不带参数的 `help()`，进入交互式帮助查看器。

注意，`help()` 不能直接用于 `for`、`if`、`while` 等基本语句。例如，`help(for)` 会导致语法错误。可以尝试将主题放入引号，如 `help("for")`。如果仍不起作用，就需要上网搜索。

后续练习：访问 <http://docs.python.org>，找到 `abs()` 的文档。提示：它位于标准库参考的内置函数部分。

### 练习 1.3：复制与粘贴

本课程由一系列传统网页组成，鼓励你**亲手输入**交互式 Python 示例。如果第一次学习 Python，建议采用这种“慢方法”：放慢速度，输入代码，并思考自己在做什么，能更好地体会这门语言。

如果必须复制粘贴示例，请从 `>>>` 提示符之后开始选择，到第一个空行或下一个 `>>>` 之前为止，以先出现者为准。在浏览器中选择“复制”，切换到 Python 窗口并选择“粘贴”。粘贴后可能还需按一次回车才能执行。

通过复制粘贴执行以下会话中的 Python 语句：

```python
>>> 12 + 20
32
>>> (3 + 4
         + 5 + 6)
18
>>> for i in range(5):
        print(i)

0
1
2
3
4
>>>
```

警告：基础 Python shell 一次不能粘贴多条 Python 命令，即 `>>>` 后的语句。必须逐条粘贴。

完成后请记住：慢慢输入代码并思考，比直接复制粘贴能让你从课程中获得更多。

### 练习 1.4：我的公交车在哪里？

说明：这是个有趣的例子，当年在办公室授课时很受欢迎。你可以查询公交车，然后亲眼看到它从窗外经过。可惜，API 很少能一直存在，这个接口似乎也已经退出历史舞台。——Dave

更新：GitHub 用户 @asett 提出了以下修改，可能可以运行，但需要提供自己的 API 密钥（可从[这里](https://www.transitchicago.com/developers/bustracker/)获取）。

```python
import urllib.request
u = urllib.request.urlopen('http://www.ctabustracker.com/bustime/api/v2/getpredictions?key=ADD_YOUR_API_KEY_HERE&rt=22&stpid=14791')
from xml.etree.ElementTree import parse
doc = parse(u)
print("Arrival time in minutes:")
for pt in doc.findall('.//prdctdn'):
        print(pt.text)
```

（以下为原始练习示例。）

尝试更高级的操作：输入以下语句，查询在芝加哥 Clark 街和 Balmoral 街交叉口等待北向 CTA \#22 公交车的人还要等多久：

```python
>>> import urllib.request
>>> u = urllib.request.urlopen('http://ctabustracker.com/bustime/map/getStopPredictions.jsp?stop=14791&route=22')
>>> from xml.etree.ElementTree import parse
>>> doc = parse(u)
>>> for pt in doc.findall('.//pt'):
        print(pt.text)

6 MIN
18 MIN
28 MIN
>>>
```

没错，你刚用大约 6 行代码下载网页、解析 XML 文档，并提取了有用信息。访问的数据实际上也用于 <http://ctabustracker.com/bustime/home.jsp>。再次运行，观察预计到站时间如何变化。

注意：服务只报告未来 30 分钟内的到站时间。如果你在其他时区，而芝加哥恰好是凌晨 3 点，可能没有任何输出。可以用上面的公交追踪链接核实。

如果第一条 `import urllib.request` 失败，你可能正在使用 Python 2。本课程要求 Python 3.6 或更新版本，如有需要，请到 <https://www.python.org> 下载。

如果工作环境要求使用 HTTP 代理，可能需要设置 `HTTP_PROXY` 环境变量，才能完成这部分练习。例如：

```python
>>> import os
>>> os.environ['HTTP_PROXY'] = 'http://yourproxy.server.com'
>>>
```

如果无法运行，也不用担心。本课程其余部分与 XML 解析无关。

[目录](../Contents.md) \| [下一节（1.2 第一个程序）](02_Hello_world.md)
