# 将数据存入文件

在[《文件(1)》](./126.md)和[《文件(2)》](./127.md)中，已经学习了如何读写文件。

如果在程序中，有数据要保存到磁盘中，放到某个文件中是一种不错的方法。但是，如果像以前那样存，未免有点凌乱，并且没有什么良好的存储格式，导致数据以后被读出来的时候遇到麻烦，特别是不能让另外的使用者很好地理解。不要忘记了，编程是一个合作的活。还有，存储的数据不一定都是类似字符串、整数那种基础类型的。

总而言之，需要将要存储的对象格式化（或者叫做序列化），才好存好取。这就有点类似集装箱的作用。

所以，要用到本讲中提供的方式。

## pickle

pickle 是标准库中的一个模块，还有跟它完全一样的叫做 cpickle，两者的区别就是后者更快。所以，下面操作中，不管是用 `import pickle`，还是用 `import cpickle as pickle`，在功能上都是一样的。

    >>> import pickle
    >>> integers = [1, 2, 3, 4, 5]
    >>> f = open("22901.dat", "wb")
    >>> pickle.dump(integers, f)
    >>> f.close()

用 `pickle.dump(integers, f)` 将数据 integers 保存到了文件 22901.dat 中。如果你要打开这个文件，看里面的内容，可能有点失望，但是，它对计算机是友好的。这个步骤，可以称之为将对象序列化。用到的方法是：

`pickle.dump(obj,file[,protocol])`

- obj：序列化对象，上面的例子中是一个列表，它是基本类型，也可以序列化自己定义的类型。
- file：一般情况下是要写入的文件。更广泛地可以理解为为拥有 write() 方法的对象，并且能接受字符串为为参数，所以，它还可以是一个 StringIO 对象，或者其它自定义满足条件的对象。
- protocol：可选项。默认为 False（或者说 0），是以 ASCII 格式保存对象；如果设置为 1 或者 True，则以压缩的二进制格式保存对象。

下面换一种数据格式，并且做对比：

    >>> import pickle
    >>> d = {}
    >>> integers = range(9999)
    >>> d["i"] = integers        #下面将这个 dict 格式的对象存入文件
    
    >>> f = open("22902.dat", "wb")
    >>> pickle.dump(d, f)           #文件中以 ascii 格式保存数据
    >>> f.close()

    >>> f = open("22903.dat", "wb")
    >>> pickle.dump(d, f, True)     #文件中以二进制格式保存数据
    >>> f.close()

    >>> import os
    >>> s1 = os.stat("22902.dat").st_size    #得到两个文件的大小
    >>> s2 = os.stat("22903.dat").st_size
    
    >>> print "%d, %d, %.2f%%" % (s1, s2, (s2+0.0)/s1*100)
    68903, 29774, 43.21%

比较结果发现，以二进制方式保存的文件比以 ascii 格式保存的文件小很多，前者约是后者的 43%。

所以，在序列化的时候，特别是面对较大对象时，建议将 dump() 的参数 True 设置上，虽然现在存储设备的价格便宜，但是能省还是省点比较好。

存入文件，仅是一个目标，还有另外一个目标，就是要读出来，也称之为反序列化。

    >>> integers = pickle.load(open("22901.dat", "rb"))
    >>> print integers
    [1, 2, 3, 4, 5]

就是前面存入的那个列表。再看看被以二进制存入的那个文件：

    >>> f = open("22903.dat", "rb")
    >>> d = pickle.load(f)
    >>> print d
    {'i': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, ....   #省略后面的数字}
    >>> f.close()
    
还是有自己定义数据类型的需要，这种类型是否可以用上述方式存入文件并读出来呢？看下面的例子：

    >>> import cPickle as pickle        #cPickle 更快
    >>> import StringIO                 #标准库中的一个模块，跟 file 功能类似，只不过是在内存中操作“文件”
    
    >>> class Book(object):             #自定义一种类型
    ...     def __init__(self,name):
    ...         self.name = name
    ...     def my_book(self):
    ...         print "my book is: ", self.name
    ... 

    >>> pybook = Book("<from beginner to master>")
    >>> pybook.my_book()
    my book is:  <from beginner to master>

    >>> file = StringIO.StringIO()
    >>> pickle.dump(pybook, file, 1)
    >>> print file.getvalue()           #查看“文件”内容，注意下面不是乱码
    ccopy_reg
    _reconstructor
    q(c__main__
    Book
    qc__builtin__
    object
    qNtRq}qUnameqU<from beginner to master>sb.

    >>> pickle.dump(pybook, file)       #换一种方式，再看内容，可以比较一下
    >>> print file.getvalue()           #视觉上，两者就有很大差异
    ccopy_reg
    _reconstructor
    q(c__main__
    Book
    qc__builtin__
    object
    qNtRq}qUnameqU<from beginner to master>sb.ccopy_reg
    _reconstructor
    p1
    (c__main__
    Book
    p2
    c__builtin__
    object
    p3
    NtRp4
    (dp5
    S'name'
    p6
    S'<from beginner to master>'
    p7
    sb.

如果要从文件中读出来：

    >>> file.seek(0)       #找到对应类型  
    >>> pybook2 = pickle.load(file)
    >>> pybook2.my_book()
    my book is:  <from beginner to master>
    >>> file.close()

## shelve

pickle 模块已经表现出它足够好的一面了。不过，由于数据的复杂性，pickle 只能完成一部分工作，在另外更复杂的情况下，它就稍显麻烦了。于是，又有了 shelve。

shelve 模块也是标准库中的。先看一下基本操作：写入和读取

    >>> import shelve
    >>> s = shelve.open("22901.db")
    >>> s["name"] = "www.itdiffer.com"
    >>> s["lang"] = "python"
    >>> s["pages"] = 1000
    >>> s["contents"] = {"first":"base knowledge","second":"day day up"}
    >>> s.close()

以上完成了数据写入的过程。其实，这更接近数据库的样式了。下面是读取。

    >>> s = shelve.open("22901.db")
    >>> name = s["name"]
    >>> print name
    www.itdiffer.com
    >>> contents = s["contents"]
    >>> print contents
    {'second': 'day day up', 'first': 'base knowledge'}

当然，也可以用 for 语句来读：

    >>> for k in s:
    ...     print k, s[k]
    ... 
    contents {'second': 'day day up', 'first': 'base knowledge'}
    lang python
    pages 1000
    name www.itdiffer.com

不管是写，还是读，都似乎要简化了。所建立的对象s，就如同字典一样，可称之为类字典对象。所以，可以如同操作字典那样来操作它。

但是，要小心坑：

    >>> f = shelve.open("22901.db")
    >>> f["author"]
    ['qiwsir']
    >>> f["author"].append("Hetz")    #试图增加一个
    >>> f["author"]                   #坑就在这里
    ['qiwsir']
    >>> f.close()

当试图修改一个已有键的值时，没有报错，但是并没有修改成功。要填平这个坑，需要这样做：
    
    >>> f = shelve.open("22901.db", writeback=True)    #多一个参数 True
    >>> f["author"].append("Hetz")
    >>> f["author"]                   #没有坑了
    ['qiwsir', 'Hetz']
    >>> f.close()

还用 for 循环一下：

    >>> f = shelve.open("22901.db")
    >>> for k,v in f.items():
    ...     print k,": ",v
    ... 
    contents :  {'second': 'day day up', 'first': 'base knowledge'}
    lang :  python
    pages :  1000
    author :  ['qiwsir', 'Hetz']
    name :  www.itdiffer.com

shelve 更像数据库了。

不过，它还不是真正的数据库。真正的数据库在后面。

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：第三方库](./228.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：mysql数据库(1)](./230.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。