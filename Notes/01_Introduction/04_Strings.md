[目录](../Contents.md) \| [上一节 (1.3 数字)](03_Numbers.md) \| [下一节 (1.5 列表)](05_Lists.md)

# 1.4 字符串

本节介绍处理文本的方法。

### 表示字面量文本

在程序中字符串字面量使用引号来书写。

```python
# Single quote
a = 'Yeah but no but yeah but...'

# Double quote
b = "computer says no"

# Triple quotes
c = '''
Look into my eyes, look into my eyes, the eyes, the eyes, the eyes,
not around the eyes,
don't look around the eyes,
look into my eyes, you're under.
'''
```

通常，字符串只能占一行。三引号捕获在引号结束之前的所有文本，包含所有的格式。

使用单引号（'）和双引号（“）没有区别。但是，以什么样的引号开始字符串，必须以什么样的引号结束字符串。

### 字符串转义码

转义码被用于表示控制字符和不能轻易在键盘上输入的字符。以下是一些常见的转义码：

```
'\n'      Line feed
'\r'      Carriage return
'\t'      Tab
'\''      Literal single quote
'\"'      Literal double quote
'\\'      Literal backslash
```

### 字符串表示

字符串中的每个字符在内部被存储为所谓的 Unicode “代码点（code-point）”，代码点是一个整数。可以使用下列转移序列指定确切的代码点 。

```python
a = '\xf1'          # a = 'ñ'
b = '\u2200'        # b = '∀'
c = '\U0001D122'    # c = '𝄢'
d = '\N{FOR ALL}'   # d = '∀'
```

所有可用的字符码请参考 [Unicode 字符数据库](https://unicode.org/charts) 。

### 字符串索引

可以像访问数组那样访问字符串的单个字符。你可以使用从 0 开始的整数索引，负索引指定相对于字符串尾部的位置。

```python
a = 'Hello world'
b = a[0]          # 'H'
c = a[4]          # 'o'
d = a[-1]         # 'd' (end of string)
```

你也可以指定一个索引范围来切割或者选择子串：

```python
d = a[:5]     # 'Hello'
e = a[6:]     # 'world'
f = a[3:8]    # 'lo wo'
g = a[-5:]    # 'world'
```

不包括结尾索引处的字符。缺失的索引假定为字符串的开始或者结尾。

### 字符串操作

字符串的操作包括：拼接，长度计算，成员判断和复制。

```python
# Concatenation (+)
a = 'Hello' + 'World'   # 'HelloWorld'
b = 'Say ' + a          # 'Say HelloWorld'

# Length (len)
s = 'Hello'
len(s)                  # 5

# Membership test (`in`, `not in`)
t = 'e' in s            # True
f = 'x' in s            # False
g = 'hi' not in s       # True

# Replication (s * n)
rep = s * 5             # 'HelloHelloHelloHelloHello'
```

### 字符串的方法

字符串具有对数据执行各种操作的方法。

示例：删除开头或者结尾处的任何空白。

```python
s = '  Hello '
t = s.strip()     # 'Hello'
```

示例：大小写转换。

```python
s = 'Hello'
l = s.lower()     # 'hello'
u = s.upper()     # 'HELLO'
```

示例：文本替换。

```python
s = 'Hello world'
t = s.replace('Hello' , 'Hallo')   # 'Hallo world'
```

**更多字符串方法:**

字符串具有各种各样的方法用于测试和处理文本数据。

下面是字符串方法的一小部分示例：

```python
s.endswith(suffix)     # Check if string ends with suffix
s.find(t)              # First occurrence of t in s
s.index(t)             # First occurrence of t in s
s.isalpha()            # Check if characters are alphabetic
s.isdigit()            # Check if characters are numeric
s.islower()            # Check if characters are lower-case
s.isupper()            # Check if characters are upper-case
s.join(slist)          # Join a list of strings using s as delimiter
s.lower()              # Convert to lower case
s.replace(old,new)     # Replace text
s.rfind(t)             # Search for t from end of string
s.rindex(t)            # Search for t from end of string
s.split([delim])       # Split string into list of substrings
s.startswith(prefix)   # Check if string starts with prefix
s.strip()              # Strip leading/trailing space
s.upper()              # Convert to upper case
```

### 字符串的可变性

字符串是“不可变的”或者说是只读的。一旦创建，字符串的值就无法修改。

```python
>>> s = 'Hello World'
>>> s[1] = 'a'
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>>
```

**所有处理字符串数据的操作和方法始终会创建一个新的字符串。**

### 字符串转换

使用 `str()` 函数可以将任何值转换为字符串。 `str()` 函数得到的结果是一个字符串，该字符串包含的文本与 `print()` 语句产生的文本相同。

```python
>>> x = 42
>>> str(x)
'42'
>>>
```

### 字节字符串

通常，在底层 I/O 中会遇到 8 位字节的字符串（译注：字节字符串），它是这样写的：

```python
data = b'Hello World\r\n'
```

通过把小写的 b 放到第一个引号之前来指定一个字节字符串而不是文本字符串（**译注：在字符串前面加 b 表示这是使用 ASCII 编码的字节字符串**）。大部分常用的文本字符串操作可应用于字节字符串。

```python
len(data)                         # 13
data[0:5]                         # b'Hello'
data.replace(b'Hello', b'Cruel')  # b'Cruel World\r\n'
```

字节字符串索引有点不同，因为它返回的是整数形式的字节值：

```python
data[0]   # 72 (ASCII code for 'H')
```

字节字符串与文本字符串之间的转换：

```python
text = data.decode('utf-8') # bytes -> text
data = text.encode('utf-8') # text -> bytes
```

 `'utf-8'` 这个参数指定了字符的编码方式。其它常见的编码方式有  `'ascii'` 和 `'latin1'`。

### 原始字符串

原始字符串是未解释的带有反斜杠的字符串字面量。通过在原始引号之前添加 “r” 前缀来指定。

```python
>>> rs = r'c:\newdata\test' # Raw (uninterpreted backslash)
>>> rs
'c:\\newdata\\test'
```

输出的字符串是包含在引号里面的字面量文本，与输入的文本完全相同。这在反斜杠有特殊意义的情况下很有用。例如：文件名、正则表达式等。

### f-Strings

具有格式化表达式替换的字符串。

```python
>>> name = 'IBM'
>>> shares = 100
>>> price = 91.1
>>> a = f'{name:>10s} {shares:10d} {price:10.2f}'
>>> a
'       IBM        100      91.10'
>>> b = f'Cost = ${shares*price:0.2f}'
>>> b
'Cost = $9110.00'
>>>
```

**注意: 这要求 Python 3.6 或者更新的版本.**  格式化代码的含义稍后介绍。

## 练习

在这些习题中，你将尝试对 Python 字符串类型进行操作。你应该在 Python 交互提示符下操作，在该提示符下可以轻松地查看到结果。重要提示：

> 在应该与解释器进行交互的习题中，
> `>>> `当 Python 希望你输入一个新的语句， 你将获得一个解释器提示符。习题中某些语句会跨越多行——要使这些语句执行，你可能需要多按几次回车键。提醒你，在做这些示例时，请勿输入 `>>>` 提示符。

通过定义一个包含一系列股票代号的字符串开始吧。字符串如下所示：

```python
>>> symbols = 'AAPL,IBM,MSFT,YHOO,SCO'
>>>
```

### 练习 1.13：提取单个字符和子串

字符串是字符数组。尝试提取一些字符：

```python
>>> symbols[0]
?
>>> symbols[1]
?
>>> symbols[2]
?
>>> symbols[-1]        # Last character
?
>>> symbols[-2]        # Negative indices are from end of string
?
>>>
```

在 Python 语言中，字符串是只读的。

尝试通过将  `symbols` 字符串的第一个字符变为小写字母 ‘a’ 来验证这一点。

```python
>>> symbols[0] = 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>>
```

### 练习 1.14：字符串拼接

尽管字符串数据是只读的，但是你始终可以将变量重新分配给新创建的字符串。

尝试下面的语句，该语句将一个新的股票代码 “GOOG” 拼接到 `symbols` 字符串的末尾。

```python
>>> symbols = symbols + 'GOOG'
>>> symbols
'AAPL,IBM,MSFT,YHOO,SCOGOOG'
>>>
```

糟糕！这不是我们想要的。修改它使得变量 `symbols`  保存的值为 `'AAPL,IBM,MSFT,YHOO,SCO,GOOG'`。

```python
>>> symbols = ?
>>> symbols
'AAPL,IBM,MSFT,YHOO,SCO,GOOG'
>>>
```

把 `'HPQ'` 添加到 `symbols`  字符串的前面：

```python
>>> symbols = ?
>>> symbols
'HPQ,AAPL,IBM,MSFT,YHOO,SCO,GOOG'
>>>
```

在这些示例中，表面上看起来原始字符串像正在被修改，明显违反了字符串是只读的。实际上不是这样的。每次，这些操作都会创建一个全新的字符串。当变量名 `symbols` 被重新分配，它会指向一个新创建的字符串。然后，旧的字符串被销毁，因为它不再被使用了。

### 练习 1.15：成员测试（子串测试）

尝试使用  `in`  操作符检查子串。请在交互提示符下尝试这些操作。

```python
>>> 'IBM' in symbols
?
>>> 'AA' in symbols
True
>>> 'CAT' in symbols
?
>>>
```

为什么检查 `AA` 的时候返回 `True` ?

### 练习 1.16：字符串方法

在 Python 交互提示符下，尝试一些新的字符串方法。

```python
>>> symbols.lower()
?
>>> symbols
?
>>>
```

请记住，字符串始终是只读的。如果你想要保存操作的结果，你需要把它放置到一个变量中。

```python
>>> lowersyms = symbols.lower()
>>>
```

请尝试更多的操作：

```python
>>> symbols.find('MSFT')
?
>>> symbols[13:17]
?
>>> symbols = symbols.replace('SCO','DOA')
>>> symbols
?
>>> name = '   IBM   \n'
>>> name = name.strip()    # Remove surrounding whitespace
>>> name
?
>>>
```

### 练习 1.17：f-strings

有时你想创建一个字符串并把其它变量的值嵌入到其中。

要做到这点，可以使用 f-strings。示例：

```python
>>> name = 'IBM'
>>> shares = 100
>>> price = 91.1
>>> f'{shares} shares of {name} at ${price:0.2f}'
'100 shares of IBM at $91.10'
>>>
```

从 [练习 1.10](03_Numbers.md) 中修改 mortgage.py 程序来使用 f-strings 创建它的输出。

尝试实现它，使得输出能够很好地对齐。

### 练习 1.18：正则表达式

基本字符串操作的一个局限性在于它们不支持任何类型的高级模式匹配。为此，你需要使用 Python 的 `re` 模块和正则表达式。正则表达式处理是一个大的主题，这里只是一个简短的示例：

```python
>>> text = 'Today is 3/27/2018. Tomorrow is 3/28/2018.'
>>> # Find all occurrences of a date
>>> import re
>>> re.findall(r'\d+/\d+/\d+', text)
['3/27/2018', '3/28/2018']
>>> # Replace all occurrences of a date with replacement text
>>> re.sub(r'(\d+)/(\d+)/(\d+)', r'\3-\1-\2', text)
'Today is 2018-3-27. Tomorrow is 2018-3-28.'
>>>
```

有关 `re` 模块的更多信息，请查看官方文档：[https://docs.python.org/library/re.html](https://docs.python.org/3/library/re.html)。

### 说明

当你开始尝试使用解释器时，你总是希望了解更多有关不同对象所支持的操作。例如，如何找出哪些操作是对字符串是有效的？

根据你的 Python 环境，你可能可以通过 tab 键补全来查看可用方法的列表。例如，尝试输入下面的代码：

```python
>>> s = 'hello world'
>>> s.<tab key>
>>>
```

如果单击 tab 键没有任何作用，你可以使用 Python 的内建函数 `dir()`。示例：

```python
>>> s = 'hello'
>>> dir(s)
['__add__', '__class__', '__contains__', ..., 'find', 'format',
'index', 'isalnum', 'isalpha', 'isdigit', 'islower', 'isspace',
'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'partition',
'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit',
'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase',
'title', 'translate', 'upper', 'zfill']
>>>
```

`dir()` 函数生成一个在 `(.)` 后出现的所有操作的列表。

使用  `help()` 函数可以获取有关特定操作的更多信息。

```python
>>> help(s.upper)
Help on built-in function upper:

upper(...)
    S.upper() -> string

    Return a copy of the string S converted to uppercase.
>>>
```

[目录](../Contents.md) \| [上一节 (1.3 数字)](03_Numbers.md) \| [下一节 (1.5 列表)](05_Lists.md)
