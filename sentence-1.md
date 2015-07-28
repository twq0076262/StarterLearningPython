# 语句(1)

数据类型已经学的差不多了，但是，到现在为止我们还不能真正的写程序，这就好比小学生学习写作一样，到目前为止仅仅学会了一些词语，还不知道如何造句子。从现在开始就学习如何造句子了。

在编程语言中，句子被称之为“语句”，

## 什么是语句

事实上，前面已经用过语句了，最典型的那句：`print "Hello, World"`就是语句。

为了能够严谨地阐述这个概念，抄一段[维基百科中的词条：命令式编程](http://zh.wikipedia.org/wiki/%E6%8C%87%E4%BB%A4%E5%BC%8F%E7%B7%A8%E7%A8%8B)

>命令式编程（英语：Imperative programming），是一种描述电脑所需作出的行为的编程范型。几乎所有电脑的硬件工作都是指令式的；几乎所有电脑的硬件都是设计来运行机器码，使用指令式的风格来写的。较高级的指令式编程语言使用变量和更复杂的语句，但仍依从相同的范型。

>运算语句一般来说都表现了在存储器内的数据进行运算的行为，然后将结果存入存储器中以便日后使用。高级命令式编程语言更能处理复杂的表达式，可能会产生四则运算和函数计算的结合。

一般所有高级语言，都包含如下语句，Python 也不例外：

- 循环语句:容许一些语句反复运行数次。循环可依据一个默认的数目来决定运行这些语句的次数；或反复运行它们，直至某些条件改变。
- 条件语句:容许仅当某些条件成立时才运行某个区块。否则，这个区块中的语句会略去，然后按区块后的语句继续运行。
- 无条件分支语句容许运行顺序转移到程序的其他部分之中。包括跳跃（在很多语言中称为 Goto）、副程序和 Procedure 等。

循环、条件分支和无条件分支都是控制流程。

当然，Python 中的语句还是有 Python 特别之处的（别的语言中，也会有自己的特色）。下面就开始娓娓道来。

## print

在 Python2.x 中，print 是一个语句，但是在 Python3.x 中它是一个函数了。这点请注意。不过，这里所使用的还是 Python2.x。

>为什么不用 Python3.x？这个问题在开始就回答过。但是还有朋友问。重复回答：因为现在很多工程项目都是 Python2.x，Python3.x 相对 Python2.x 有不完全兼容的地方。学 Python 的目的就是要在真实的工程项目中使用，理所应当要学 Python2.x。此外，学会了 Python2.x，将来过渡到 Python3.x，只需要注意一些细节即可。

print 发起的语句，在程序中主要是将某些东西打印出来，还记得在讲解字符串的时候，专门讲述了字符串的格式化输出吗？那就是用来 print 的。

    >>> print "hello, world"
    hello, world
    >>> print "hello","world"
    hello world

请仔细观察，上面两个 print 语句的差别。第一个打印的是"hello, world"，包括其中的逗号和空格，是一个完整的字符串。第二个打印的是两个字符串，一个是"hello"，另外一个是"world"，两个字符串之间用逗号分隔。

本来，在 print 语句中，字符串后面会接一个 `\n` 符号。即换行。但是，如果要在一个字符串后面跟着逗号，那么换行就取消了，意味着两个字符串"hello"，"world"打印在同一行。

或许现在体现的还不时很明显，如果换一个方法，就显示出来了。（下面用到了一个被称之为循环的语句，下一节会重点介绍。

    >>> for i in [1,2,3,4,5]:
    ...     print i
    ... 
    1
    2
    3
    4
    5
    
这个循环的意思就是要从列表中依次取出每个元素，然后赋值给变量 i，并用 print 语句打印打出来。在变量 i 后面没有任何符号，每打印一个，就换行，再打印另外一个。

下面的方式就跟上面的有点区别了。

    >>> for i in [1,2,3,4,5]:
    ...     print i ,
    ... 
    1 2 3 4 5

就是在 print 语句的最后加了一个逗号，打印出来的就在一行了。

print 语句经常用在调试程序的过程，让我们能够知道程序在执行过程中产生的结果。

## import

在[《常用数学函数和运算优先级》](./104.md)中，曾经用到过一个 math 模块，它能提供很多数学函数，但是这些函数不是 Python 的内建函数，是 math 模块的，所以，要用 import 引用这个模块。

这种用 import 引入模块的方法，是 Python 编程经常用到的。引用方法有如下几种：

    >>> import math
    >>> math.pow(3,2)
    9.0

这是常用的一种方式，而且非常明确，`math.pow(3,2)`就明确显示了，pow()函数是 math 模块里的。可以说这是一种可读性非常好的引用方式，并且不同模块的同名函数不会产生冲突。

    >>> from math import pow
    >>> pow(3,2)
    9.0

这种方法就有点偷懒了，不过也不难理解，从字面意思就知道 pow()函数来自于 math 模块。在后续使用的时候，只需要直接使用 `pow()`即可，不需要在前面写上模块名称了。这种引用方法，比较适合于引入模块较少的时候。如果引入模块多了，可读性就下降了，会不知道那个函数来自那个模块。

    >>> from math import pow as pingfang
    >>> pingfang(3,2)
    9.0
这是在前面那种方式基础上的发展，将从某个模块引入的函数重命名，比如讲 pow 充命名为 pingfang，然后使用 `pingfang()`就相当于在使用 `pow()`了。

如果要引入多个函数，可以这样做：

    >>> from math import pow, e, pi
    >>> pow(e,pi)
    23.140692632779263

引入了 math 模块里面的 pow,e,pi，pow()是一个乘方函数，e，就是那个欧拉数；pi 就是 π.

>e，作为数学常数，是自然对数函数的底数。有时称他为欧拉函数（Euler's number），以瑞士数学家欧拉命名；也有个较鲜见的名字纳皮尔常数，以纪念苏格兰数学家约翰·纳皮尔引进对数。它是一个无限不循环小数。e = 2.71828182845904523536(《维基百科》)

>e 的 π 次方,是一个数学常数。与 e 和 π 一样，它是一个超越数。这个常数在希尔伯特第七问题中曾提到过。(《维基百科》)

    >>> from math import *
    >>> pow(3,2)
    9.0
    >>> sqrt(9)
    3.0

这种引入方式是最贪图省事的了，一下将 math 中的所有函数都引过来了。不过，这种方式的结果是让可读性更降低了。仅适用于模块中的函数比较少的时候，并且在程序中应用比较频繁。

在这里，我们用 math 模块为例，引入其中的函数。事实上，不仅函数可以引入，模块中还可以包括常数等，都可以引入。在编程中，模块中可以包括各样的对象，都可以引入。

## 赋值语句

对于赋值语句，应该不陌生，在前面已经频繁使用了，如 `a = 3` 这样的，就是将一个整数赋给了变量。

>编程中的“=”和数学中的“=”是完全不同的。在编程语言中，“=”表示赋值过程。

除了那种最简单的赋值之外，还可以这么干：

    >>> x, y, z = 1, "python", ["hello", "world"]
    >>> x
    1
    >>> y
    'python'
    >>> z
    ['hello', 'world']

这里就一一对应赋值了。如果把几个值赋给一个，可以吗？

    >>> a = "itdiffer.com", "python"

    >>> a
    ('itdiffer.com', 'python')

原来是将右边的两个值装入了一个元组，然后将元组赋给了变量 a。这个 Python 太聪明了。

在 Python 的赋值语句中，还有一个更聪明的，它一出场，简直是让一些已经学习过某种其它语言的人亮瞎眼。

有两个变量，其中 `a = 2`,`b = 9`。现在想让这两个变量的值对调，即最终是 `a = 9`,`b = 2`.

这是一个简单而经典的题目。在很多编程语言中，是这么处理的：

    temp = a;
    a = b;
    b = temp;
    
这么做的那些编程语言，变量就如同一个盒子，值就如同放到盒子里面的东西。如果要实现对调，必须在找一个盒子，将 a 盒子里面的东西（数字 2）拿到那个临时盒子(temp)中，这样 a 盒子就空了，然后将 b 盒子中的东西拿(数字 9)拿到 a 盒子中(a = b)，完成这步之后，b 盒子是空的了，最后将临时盒子里面的那个数字 2 拿到 b 盒子中。这就实现了两个变量值得对调。

太啰嗦了。

Python 只要一行就完成了。

    >>> a = 2
    >>> b = 9

    >>> a, b = b, a
    
    >>> a
    9
    >>> b
    2

`a, b = b, a` 就实现了数值对调，多么神奇。之所以神奇，就是因为我前面已经数次提到的 Python 中变量和数据对象的关系。变量相当于贴在对象上的标签。这个操作只不过是将标签换个位置，就分别指向了不同的数据对象。

还有一种赋值方式，被称为“链式赋值”

    >>> m = n = "I use python"
    >>> print m,n
    I use python I use python

用这种方式，实现了一次性对两个变量赋值，并且值相同。

    >>> id(m)
    3072659528L
    >>> id(n)
    3072659528L

用 `id()`来检查一下，发现两个变量所指向的是同一个对象。

另外，还有一种判断方法，来检查两个变量所指向的值是否是同一个（注意，同一个和相等是有差别的。在编程中，同一个就是 `id()`的结果一样。

    >>> m is n
    True

这是在检查 m 和 n 分别指向的对象是否是同一个，True 说明是同一个。
    
    >>> a = "I use python"
    >>> b = a
    >>> a is b
    True

这是跟上面链式赋值等效的。

但是：

    >>> b = "I use python"
    >>> a is b
    False
    >>> id(a)
    3072659608L
    >>> id(b)
    3072659568L
    
    >>> a == b
    True

看出其中的端倪了吗？这次 a、b 两个变量虽然相等，但不是指向同一个对象。

还有一种赋值形式，如果从数学的角度看，是不可思议的，如：`x = x + 1`，在数学中，这个等式是不成立的。因为数学中的“=”是等于的含义，但是在编程语言中，它成立，因为"="是赋值的含义，即将变量 x 增加 1 之后，再把得到的结果赋值变量 x.

这种变量自己变化之后将结果再赋值给自己的形式，称之为“增量赋值”。+、-、*、/、% 都可以实现这种操作。

为了让这个操作写起来省点事（要写两遍同样一个变量），可以写成：`x += 1`

    >>> x = 9
    >>> x += 1
    >>> x
    10
    
除了数字，字符串进行增量赋值，在实际中也很有价值。

    >>> m = "py"
    >>> m += "th"
    >>> m
    'pyth'
    >>> m += "on"
    >>> m
    'python'

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：运算符](./120.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：语句(2)](./122.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。