# 迭代器

迭代，对于读者已经不陌生了，曾有专门一节来讲述，如果印象不深，请复习[《迭代》](./128.md)。

正如读者已知，对序列（列表、元组）、字典和文件都可以用 `iter()` 方法生成迭代对象，然后用 `next()` 方法访问。当然，这种访问不是自动的，如果用 for 循环，就可以自动完成上述访问了。

如果用 `dir(list)`,`dir(tuple)`,`dir(file)`,`dir(dict)` 来查看不同类型对象的属性，会发现它们都有一个名为`__iter__`的东西。这个应该引起读者的关注，因为它和迭代器（iterator）、内置的函数 iter() 在名字上是一样的，除了前后的双下划线。望文生义，我们也能猜出它肯定是跟迭代有关的东西。当然，这种猜测也不是没有根据的，其重要根据就是英文单词，如果它们之间没有一点关系，肯定不会将命名搞得一样。

猜对了。`__iter__`就是对象的一个特殊方法，它是迭代规则(iterator potocol)的基础。或者说，对象如果没有它，就不能返回迭代器，就没有 `next()` 方法，就不能迭代。

>提醒注意，如果读者用的是 Python3.x，迭代器对象实现的是`__next__()` 方法，不是 `next()`。并且，在 Python3.x 中有一个内建函数 next()，可以实现 `next(it)`，访问迭代器，这相当于于 python2.x 中的 `it.next()`（it 是迭代对象）。

那些类型是 list、tuple、file、dict 对象有`__iter__()`方法，标着他们能够迭代。这些类型都是 Python 中固有的，我们能不能自己写一个对象，让它能够迭代呢？

当然呢！要不然 python 怎么强悍呢。

    #!/usr/bin/env Python
    # coding=utf-8

    """
    the interator as range()
    """
    class MyRange(object):
        def __init__(self, n):
            self.i = 0
            self.n = n

        def __iter__(self):
            return self

        def next(self):
            if self.i < self.n:
                i = self.i
                self.i += 1
                return i
            else:
                raise StopIteration()

    if __name__ == "__main__":
        x = MyRange(7)
        print "x.next()==>", x.next()
        print "x.next()==>", x.next()
        print "------for loop--------"
        for i in x:
            print i

将代码保存，并运行，结果是：

    $ python 21401.py 
    x.next()==> 0
    x.next()==> 1
    ------for loop--------
    2
    3
    4
    5
    6

以上代码的含义，是自己仿写了拥有 `range()` 的对象，这个对象是可迭代的。分析如下：

类 MyRange 的初始化方法`__init__()` 就不用赘述了，因为前面已经非常详细分析了这个方法，如果复习，请阅读[《类(2)》](./207md)相关内容。

`__iter__()` 是类中的核心，它返回了迭代器本身。一个实现了`__iter__()`方法的对象，即意味着其实可迭代的。

含有 `next()` 的对象，就是迭代器，并且在这个方法中，在没有元素的时候要发起 `StopIteration()` 异常。

如果对以上类的调用换一种方式：

    if __name__ == "__main__":
        x = MyRange(7)
        print list(x)
        print "x.next()==>", x.next()

运行后会出现如下结果：

    $ python 21401.py 
    [0, 1, 2, 3, 4, 5, 6]
    x.next()==>
    Traceback (most recent call last):
      File "21401.py", line 26, in <module>
        print "x.next()==>", x.next()
      File "21401.py", line 21, in next
        raise StopIteration()
    StopIteration

说明什么呢？`print list(x)` 将对象返回值都装进了列表中并打印出来，这个正常运行了。此时指针已经移动到了迭代对象的最后一个，正如在[《迭代》](./128.md)中描述的那样，`next()` 方法没有检测也不知道是不是要停止了，它还要继续下去，当继续下一个的时候，才发现没有元素了，于是返回了 `StopIteration()`。

为什么要将用这种可迭代的对象呢？就像上面例子一样，列表不是挺好的吗？

列表的确非常好，在很多时候效率很高，并且能够解决相当普遍的问题。但是，不要忘记一点，在某些时候，列表可能会给你带来灾难。因为在你使用列表的时候，需要将列表内容一次性都读入到内存中，这样就增加了内存的负担。如果列表太大太大，就有内存溢出的危险了。这时候需要的是迭代对象。比如斐波那契数列（在本教程多处已经提到这个著名的数列：[《练习》的练习 4](./129.md)，[《函数(4)》中递归举例](./204.md)）:

    #!/usr/bin/env Python
    # coding=utf-8
    """
    compute Fibonacci by iterator
    """
    __metaclass__ = type

    class Fibs:
        def __init__(self, max):
            self.max = max
            self.a = 0
            self.b = 1

        def __iter__(self):
            return self

        def next(self):
            fib = self.a
            if fib > self.max:
                raise StopIteration
            self.a, self.b = self.b, self.a + self.b
            return fib

    if __name__ == "__main__":
        fibs = Fibs(5)
        print list(fibs)

运行结果是：

    $ python 21402.py 
    [0, 1, 1, 2, 3, 5]

>给读者一个思考问题：要在斐波那契数列中找出大于 1000 的最小的数，能不能在上述代码基础上改造得出呢？

关于列表和迭代器之间的区别，还有两个非常典型的内建函数：`range()` 和 `xrange()`，研究一下这两个的差异，会有所收获的。

    range(...)
        range(stop) -> list of integers
        range(start, stop[, step]) -> list of integers

    >>> dir(range)
    ['__call__', '__class__', '__cmp__', '__delattr__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__self__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']

从 `range()` 的帮助文档和方法中可以看出，它的结果是一个列表。但是，如果用 `help(xrange)` 查看：

    class xrange(object)
     |  xrange(stop) -> xrange object
     |  xrange(start, stop[, step]) -> xrange object
     |  
     |  Like range(), but instead of returning a list, returns an object that
     |  generates the numbers in the range on demand.  For looping, this is 
     |  slightly faster than range() and more memory efficient.

`xrange()` 返回的是对象，并且进一步告诉我们，类似 `range()`，但不是列表。在循环的时候，它跟 `range()` 相比“slightly faster than range() and more memory efficient”，稍快并更高的内存效率（就是省内存呀）。查看它的方法：

    >>> dir(xrange)
    ['__class__', '__delattr__', '__doc__', '__format__', '__getattribute__', '__getitem__', '__hash__', '__init__', '__iter__', '__len__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']

看到令人兴奋的`__iter__`了吗？说明它是可迭代的，它返回的是一个可迭代的对象。

也就是说，通过 `range()` 得到的列表，会一次性被读入内存，而 `xrange()` 返回的对象，则是需要一个数值才从返回一个数值。比如这样一个应用：

还记得 `zip()` 吗？

    >>> a = ["name", "age"]
    >>> b = ["qiwsir", 40]
    >>> zip(a,b)
    [('name', 'qiwsir'), ('age', 40)]

如果两个列表的个数不一样，就会以短的为准了，比如：

    >>> zip(range(4), xrange(100000000))
    [(0, 0), (1, 1), (2, 2), (3, 3)]

第一个 `range(4)` 产生的列表被读入内存；第二个是不是也太长了？但是不用担心，它根本不会产生那么长的列表，因为只需要前 4 个数值，它就提供前四个数值。如果你要修改为 `range(100000000)`，就要花费时间了，可以尝试一下哦。

迭代器的确有迷人之处，但是它也不是万能之物。比如迭代器不能回退，只能如过河的卒子，不断向前。另外，迭代器也不适合在多线程环境中对可变集合使用（这句话可能理解有困难，先混个脸熟吧，等你遇到多线程问题再说）。

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：特殊方法(2)](./213.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：生成器](./215.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。