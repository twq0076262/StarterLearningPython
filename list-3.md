# 列表(3)

接着上节内容。下面是上节中说好要介绍的列表方法：

>'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort'

已经在上节讲解了前四个。

继续。

## list 函数

### insert

前面有向 list 中追加元素的方法，那个追加是且只能是将新元素添加在 list 的最后一个。如：

    >>> all_users = ["qiwsir","github"]
    >>> all_users.append("io")
    >>> all_users
    ['qiwsir', 'github', 'io']

与 `list.append(x)`类似，`list.insert(i,x)`也是对 list 元素的增加。只不过是可以在任何位置增加一个元素。

还是先看[官方文档来理解](https://docs.python.org/2/tutorial/datastructures.html)：

>list.insert(i, x)

>    Insert an item at a given position. The first argument is the index of the element before which to insert, so a.insert(0, x) inserts at the front of the list, and a.insert(len(a), x) is equivalent to a.append(x).

这次就不翻译了。如果看不懂英语，怎么了解贵国呢？一定要硬着头皮看英语，不仅能够学好程序，更能...（此处省略两千字）

根据官方文档的说明，我们做下面的实验，请看官从实验中理解：

    >>> all_users
    ['qiwsir', 'github', 'io']
    >>> all_users.insert("python")      
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: insert() takes exactly 2 arguments (1 given)
    
请注意看报错的提示信息，`insert()`应该供给两个参数，但是这里只给了一个。所以报错没商量啦。
    
    >>> all_users.insert(0,"python")
    >>> all_users
    ['python', 'qiwsir', 'github', 'io']
    
    >>> all_users.insert(1,"http://")
    >>> all_users
    ['python', 'http://', 'qiwsir', 'github', 'io']
    
`list.insert(i, x)`中的 i 是将元素 x 插入到 list 中的位置，即将 x 插入到索引值是 i 的元素前面。注意，索引是从 0 开始的。

有一种操作，挺有意思的，如下：

    >>> length = len(all_users)
    >>> length
    5       
    >>> all_users.insert(length,"algorithm")
    >>> all_users
    ['python', 'http://', 'qiwsir', 'github', 'io', 'algorithm']

在 all_users 中，没有索引最大到 4，如果要 `all_users.insert(5,"algorithm")`，则表示将`"algorithm"`插入到索引值是 5 的前面，但是没有。换个说法，5 前面就是 4 的后面。所以，就是追加了。

其实，还可以这样：

    >>> a = [1,2,3]
    >>> a.insert(9,777)
    >>> a
    [1, 2, 3, 777]

也就是说，如果遇到那个 i 已经超过了最大索引值，会自动将所要插入的元素放到列表的尾部，即追加。

### pop 和 remove

list 中的元素，不仅能增加，还能被删除。删除 list 元素的方法有两个，它们分别是：

>list.remove(x)

>    Remove the first item from the list whose value is x. It is an error if there is no such item.

>list.pop([i])

>    Remove the item at the given position in the list, and return it. If no index is specified, a.pop() removes and returns the last item in the list. (The square brackets around the i in the method signature denote that the parameter is optional, not that you should type square brackets at that position. You will see this notation frequently in the Python Library Reference.)

我这里讲授 Python，有一个习惯，就是用学习物理的方法。如果看官当初物理没有学好，那么一定是没有用这种方法，或者你的老师没有用这种教学法。这种方法就是：自己先实验，然后总结规律。

先实验 list.remove(x)，注意看上面的描述。这是一个能够删除 list 元素的方法，同时上面说明告诉我们，如果 x 没有在 list 中，会报错。

    >>> all_users
    ['Python', 'http://', 'qiwsir', 'github', 'io', 'algorithm']
    >>> all_users.remove("http://")
    >>> all_users       #的确是把"http://"删除了
    ['Python', 'qiwsir', 'github', 'io', 'algorithm']
    
    >>> all_users.remove("tianchao")        #原 list 中没有“tianchao”，要删除，就报错。
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: list.remove(x): x not in list

    >>> lst = ["python","java","python","c"]
    >>> lst.remove("python")
    >>> lst
    ['java', 'python', 'c']

重点解释一下第三个操作。哦，忘记一个提醒，我在前面的很多操作中，也都给列表的变量命名为 lst，但是不是 list,为什么呢？因为 list 是 Python 的保留字。

还是继续第三段操作，列表中有两个'Python'字符串，当删除后，发现结果只删除了第一个'Python'字符串，第二个还在。请仔细看前面的文档说明：**remove the first item ...**

注意两点：

- 如果正确删除，不会有任何反馈。没有消息就是好消息。并且是对列表进行原地修改。
- 如果所删除的内容不在 list 中，就报错。注意阅读报错信息：x not in list

>什么是保留字？在 Python 中，当然别的语言中也是如此啦。某些词语或者拼写是不能被用户拿来做变量／函数／类等命名，因为它们已经被语言本身先占用了。这些就是所谓保留字。在 Python 中，以下是保留字，不能用于你自己变成中的任何命名。

>and, assert, break, class, continue, def, del, elif, else, except, exec, finally, for, from, global, if, import, in, is, lambda, not, or, pass, print, raise, return, try, while, with,yield

>这些保留字，都是我们在编程中要用到的。有的你已经在前面遇到了。

看官是不是想到一个问题？如果能够在删除之前，先判断一下这个元素是不是在 list 中，如果在就删，不在就不删，不是更智能吗？

如果看官想到这里，就是在编程的旅程上一进步。Python 的确让我们这么做。

    >>> all_users
    ['python', 'qiwsir', 'github', 'io', 'algorithm']
    >>> "Python" in all_users       #这里用 in 来判断一个元素是否在 list中，在则返回 True，否则返回False
    True
    
    >>> if "Python" in all_users:
    ...     all_users.remove("python")
    ...     print all_users
    ... else:
    ...     print "'Python' is not in all_users"
    ... 
    ['qiwsir', 'github', 'io', 'algorithm']     #删除了"Python"元素

    >>> if "Python" in all_users:
    ...     all_users.remove("Python")
    ...     print all_users
    ... else:
    ...     print "'Python' is not in all_users"
    ... 
    'Python' is not in all_users        #因为已经删除了，所以就没有了。

上述代码，就是两段小程序，我是在交互模式中运行的，相当于小实验。这里其实用了一个后面才会讲到的东西：if-else语句。不过，我觉得即使没有学习，你也能看懂，因为它非常接近自然语言了。

另外一个删除 list.pop([i])会怎么样呢？看看文档，做做实验。

    >>> all_users
    ['qiwsir', 'github', 'io', 'algorithm']
    >>> all_users.pop()     #list.pop([i]),圆括号里面是[i]，表示这个序号是可选的
    'algorithm'             #如果不写，就如同这个操作，默认删除最后一个，并且将该结果返回
    
    >>> all_users
    ['qiwsir', 'github', 'io']

    >>> all_users.pop(1)        #指定删除编号为 1 的元素"github"
    'github'
    
    >>> all_users
    ['qiwsir', 'io']
    >>> all_users.pop()
    'io'
    
    >>> all_users           #只有一个元素了，该元素编号是 0
    ['qiwsir']
    >>> all_users.pop(1)    #但是非要删除编号为 1 的元素，结果报错。注意看报错信息
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IndexError: pop index out of range      #删除索引超出范围，就是 1 不在 list 的编号范围之内

简单总结一下，`list.remove(x)`中的参数是列表中元素，即删除某个元素；`list.pop([i])`中的 i 是列表中元素的索引值，这个 i 用方括号包裹起来，意味着还可以不写任何索引值，如上面操作结果，就是删除列表的最后一个。

给看官留下一个思考题，如果要像前面那样，能不能事先判断一下要删除的编号是不是在 list 的长度范围（用 len(list)获取长度)以内？然后进行删除或者不删除操作。

### reverse

reverse 比较简单，就是把列表的元素顺序反过来。

    >>> a = [3,5,1,6]
    >>> a.reverse()
    >>> a
    [6, 1, 5, 3]

注意，是原地反过来，不是另外生成一个新的列表。所以，它没有返回值。跟这个类似的有一个内建函数 reversed，建议读者了解一下这个函数的使用方法。

>因为 `list.reverse()`不返回值，所以不能实现对列表的反向迭代，如果要这么做，可以使用 reversed 函数。

### sort

sort 就是对列表进行排序。帮助文档中这么写的：

>sort(...)

>    L.sort(cmp=None, key=None, reverse=False) -- stable sort *IN PLACE*;
        cmp(x, y) -> -1, 0, 1


    >>> a = [6, 1, 5, 3]
    >>> a.sort()
    >>> a
    [1, 3, 5, 6]

`list.sort()`也是让列表进行原地修改，没有返回值。默认情况，如上面操作，实现的是从小到大的排序。

    >>> a.sort(reverse=True)
    >>> a
    [6, 5, 3, 1]

这样做，就实现了从大到小的排序。

在前面的函数说明中，还有一个参数 key，这个怎么用呢？不知道看官是否用过电子表格，里面就是能够设置按照哪个关键字进行排序。这里也是如此。

    >>> lst = ["Python","java","c","pascal","basic"]
    >>> lst.sort(key=len)
    >>> lst
    ['c', 'java', 'basic', 'Python', 'pascal']

这是以字符串的长度为关键词进行排序。

对于排序，也有一个更为常用的内建函数 sorted。

顺便指出，排序是一个非常有研究价值的话题。不仅仅是现在这么一个函数。有兴趣的读者可以去网上搜一下排序相关知识。

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：列表(2)](./112.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：列表和字符串](./114.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。

