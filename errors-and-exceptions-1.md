# 错误和异常 (1)

虽然在前面的学习中，已经遇到了错误和异常问题，但是一直没有很认真的研究它。现在来近距离观察错误和异常。

## 错误

Python 中的错误之一是语法错误(syntax errors)，比如：

    >>> for i in range(10)
      File "<stdin>", line 1
        for i in range(10)
                         ^
    SyntaxError: invalid syntax

上面那句话因为缺少冒号`:`，导致解释器无法解释，于是报错。这个报错行为是由 Python 的语法分析器完成的，并且检测到了错误所在文件和行号（`File "<stdin>", line 1`），还以向上箭头`^`标识错误位置（后面缺少`:`），最后显示错误类型。

错误之二是在没有语法错误之后，会出现逻辑错误。逻辑错误可能会由于不完整或者不合法的输入导致，也可能是无法生成、计算等，或者是其它逻辑问题。

当 Python 检测到一个错误时，解释器就无法继续执行下去，于是抛出异常。

## 异常

看一个异常（让 0 做分母了，这是小学生都相信会有异常的）：

    >>> 1/0
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ZeroDivisionError: integer division or modulo by zero

当 Python 抛出异常的时候，首先有“跟踪记录(Traceback)”，还可以给它取一个更优雅的名字“回溯”。后面显示异常的详细信息。异常所在位置（文件、行、在某个模块）。

最后一行是错误类型以及导致异常的原因。

下表中列出常见的异常

|异常 |	描述|
|-----|-----|
|NameError |尝试访问一个没有申明的变量|
|ZeroDivisionError |	除数为 0|
|SyntaxError| 	语法错误|
|IndexError| 	索引超出序列范围|
|KeyError| 	请求一个不存在的字典关键字|
|IOError| 	输入输出错误（比如你要读的文件不存在）|
|AttributeError| 	尝试访问未知的对象属性|

为了能够深入理解，依次举例，展示异常的出现条件和结果。

### NameError

    >>> bar
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    NameError: name 'bar' is not defined

Python 中变量需要初始化，即要赋值。虽然不需要像某些语言那样声明，但是要赋值先。因为变量相当于一个标签，要把它贴到对象上才有意义。

### ZeroDivisionError

    >>> 1/0
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ZeroDivisionError: integer division or modulo by zero

貌似这样简单的错误时不会出现的，但在实际情境中，可能没有这么容易识别，所以，依然要小心为妙。

### SyntaxError

    >>> for i in range(10)
      File "<stdin>", line 1
        for i in range(10)
                         ^
    SyntaxError: invalid syntax

这种错误发生在 Python 代码编译的时候，当编译到这一句时，解释器不能讲代码转化为 Python 字节码，就报错。只有改正才能继续。所以，它是在程序运行之前就会出现的（如果有错）。现在有不少编辑器都有语法校验功能，在你写代码的时候就能显示出语法的正误，这多少会对编程者有帮助。

### IndexError

    >>> a = [1,2,3]
    >>> a[4]
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IndexError: list index out of range
    
    >>> d = {"python":"itdiffer.com"}
    >>> d["java"]
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: 'java'

这两个都属于“鸡蛋里面挑骨头”类型，一定得报错了。不过在编程实践中，特别是循环的时候，常常由于循环条件设置不合理出现这种类型的错误。

### IOError

    >>> f = open("foo")
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IOError: [Errno 2] No such file or directory: 'foo'

如果你确认有文件，就一定要把路径写正确，因为你并没有告诉 Python 对你的 computer 进行全身搜索，所以，Python 会按照你指定位置去找，找不到就异常。

### AttributeError

    >>> class A(object): pass
    ... 
    >>> a = A()
    >>> a.foo
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    AttributeError: 'A' object has no attribute 'foo'

属性不存在。这种错误前面多次见到。

其实，Python 内建的异常也不仅仅上面几个，上面只是列出常见的异常中的几个。比如还有：

    >>> range("aaa")
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: range() integer end argument expected, got str.

总之，如果读者在调试程序的时候遇到了异常，不要慌张，这是好事情，是 Python 在帮助你修改错误。只要认真阅读异常信息，再用 `dir()`，`help()` 或者官方网站文档、google 等来协助，一定能解决问题。

## 处理异常

在一段程序中，为了能够让程序健壮，必须要处理异常。举例：

    #!/usr/bin/env Python
    # coding=utf-8

    while 1:
        print "this is a division program."
        c = raw_input("input 'c' continue, otherwise logout:")
        if c == 'c':
            a = raw_input("first number:")
            b = raw_input("second number:")
            try:
                print float(a)/float(b)
                print "*************************"
            except ZeroDivisionError:
                print "The second number can't be zero!"
                print "*************************"
        else:
            break

运行这段程序，显示如下过程：

    $ python 21601.py 
    this is a division program.
    input 'c' continue, otherwise logout:c
    first number:5
    second number:2
    2.5
    *************************
    this is a division program.
    input 'c' continue, otherwise logout:c
    first number:5
    second number:0
    The second number can't be zero!
    *************************
    this is a division program.
    input 'c' continue, otherwise logout:d
    $
    
从运行情况看，当在第二个数，即除数为 0 时，程序并没有因为这个错误而停止，而是给用户一个友好的提示，让用户有机会改正错误。这完全得益于程序中“处理异常”的设置，如果没有“处理异常”，异常出现，就会导致程序终止。

处理异常的方式之一，使用 `try...except...`。

对于上述程序，只看 try 和 except 部分，如果没有异常发生，except 子句在 try 语句执行之后被忽略；如果 try 子句中有异常可，该部分的其它语句被忽略，直接跳到 except 部分，执行其后面指定的异常类型及其子句。

except 后面也可以没有任何异常类型，即无异常参数。如果这样，不论 try 部分发生什么异常，都会执行 except。

在 except 子句中，可以根据异常或者别的需要，进行更多的操作。比如：

    #!/usr/bin/env Python
    # coding=utf-8

    class Calculator(object):
        is_raise = False
        def calc(self, express):
            try:
                return eval(express)
            except ZeroDivisionError:
                if self.is_raise:
                    print "zero can not be division."
                else:
                    raise

在这里，应用了一个函数 `eval()`，它的含义是：

    eval(...)
        eval(source[, globals[, locals]]) -> value
    
        Evaluate the source in the context of globals and locals.
        The source may be a string representing a Python expression
        or a code object as returned by compile().
        The globals must be a dictionary and locals can be any mapping,
        defaulting to the current globals and locals.
        If only globals is given, locals defaults to it.

例如：

    >>> eval("3+5")
    8

另外，在 except 子句中，有一个 `raise`，作为单独一个语句。它的含义是将异常信息抛出。并且，except 子句用了一个判断语句，根据不同的情况确定走不同分支。            
                    
    if __name__ == "__main__":
        c = Calculator()
        print c.calc("8/0")

这时候 `is_raise = False`，则会：

    $ python 21602.py 
    Traceback (most recent call last):
      File "21602.py", line 17, in <module>
        print c.calc("8/0")
      File "21602.py", line 8, in calc
        return eval(express)
      File "<string>", line 1, in <module>
    ZeroDivisionError: integer division or modulo by zero

如果将 `is_raise` 的值改为 True，就是这样了：

    if __name__ == "__main__":
        c = Calculator()
        c.is_raise = True    #通过实例属性修改
        print c.calc("8/0")

运行结果：

    $ python 21602.py 
    zero can not be division.
    None

最后的 None 是 `c.calc("8/0")`的返回值，因为有 `print c.calc("8/0")`，所以被打印出来。

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：生成器](./215.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：错误和异常(2)](./217.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。