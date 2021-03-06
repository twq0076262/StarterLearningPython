# 函数练习

已经学习了函数的基本知识，现在练习练习。完成下面练习的原则：

1. 请读者先根据自己的设想写下代码，然后运行调试，检查得到的结果是否正确
2. 我也给出参考代码，但是，参考代码并不是最终结果
3. 读者可以在上述基础上对代码进行完善
4. 如果读者愿意，可以将代码提交到 github 上，或者到我的 QQ 群(群号:26913719)中跟大家分享讨论

## 解一元二次方程

解一元二次方程，是初中数学中的基本知识，一般来讲解法有：公式法、因式分解法等。读者可以根据自己的理解，写一段求解一元二次方程的程序。

最简单的思路就是用公式法求解，这是普适法则（普世法则？普适是否等同于普世？）。

>古巴比伦留下的陶片显示，在大约公元前 2000 年（2000 BC）古巴比伦的数学家就能解一元二次方程了。在大約公元前 480 年，中國人已经使用配方法求得了二次方程的正根，但是并没有提出通用的求解方法。公元前 300 年左右，欧几里得提出了一种更抽象的几何方法求解二次方程。

>7 世紀印度的婆罗摩笈多（Brahmagupta）是第一位懂得用使用代数方程，它同时容许有正负数的根。

>11 世紀阿拉伯的花拉子密 独立地发展了一套公式以求方程的正数解。亚伯拉罕·巴希亚（亦以拉丁文名字萨瓦索达著称）在他的著作 Liber embadorum 中，首次将完整的一元二次方程解法传入欧洲。(源自《维基百科》)

参考代码：

    #!/usr/bin/env Python
    # coding=utf-8

    """
    solving a quadratic equation
    """

    from __future__ import division
    import math

    def quadratic_equation(a,b,c):
        delta = b*b - 4*a*c
        if delta<0:
            return False
        elif delta==0:
            return -(b/(2*a))
        else:
            sqrt_delta = math.sqrt(delta)
            x1 = (-b + sqrt_delta)/(2*a)
            x2 = (-b - sqrt_delta)/(2*a)
            return x1, x2

    if __name__ == "__main__":
        print "a quadratic equation: x^2 + 2x + 1 = 0"
        coefficients = (1, 2, 1)
        roots = quadratic_equation(*coefficients)
        if roots:
            print "the result is:",roots
        else:
            print "this equation has no solution."

保存为 20501.py，并运行之：

    $ python 20501.py 
    a quadratic equation: x^2 + 2x + 1 = 0
    the result is: -1.0

能够正常运行，求解方程。

但是，如果再认真思考，发现上述代码是有很大改进空间的。至少我发现：

- 如果不小心将第一个系数(a)的值输入了 0，程序肯定会报错。如何避免之？要记住，任何人的输入都是不可靠的。
- 结果貌似只能是小数，这在某些情况下是近似值，能不能得到以分数形式表示的精确结果呢？
- 复数，Python 是可以表示复数的，如果 delta<0，是不是写成复数更好，毕竟我是学过高中数学的。

读者是否还有其它改进呢？你能不能进行改进，然后跟我和其他朋友一起来分享你的成就呢？

至少要完成上述改进，可能需要其它的有关 Python 知识，甚至于前面没有介绍。这都不要紧，掌握了基本知识之后，在编程的过程中，就要不断发挥 google 的优势，让她帮助你找寻完成任务的工具。

>Python 是一个开发的语言，很多大牛人都写了一些工具，让别人使用，减轻了后人的劳动负担。这就是所谓的第三方模块。虽然 Python 中已经有一些“自带电池”，即默认安装的，比如上面程序中用到的 math，但是我们还嫌不够。于是又很多第三方的模块来专门解决某个问题。比如这个解方程问题，就可以使用 SymPy(www.sympy.org)来解决，当然 NumPy 也是非常强悍的工具。

## 统计考试成绩

每次考试之后，教师都要统计考试成绩，一般包括：平均分，对所有人按成绩从高到低排队，谁成绩最好，谁成绩最差。还有其它的统计项，暂且不做了。只统计这几项吧。下面的任务就是读者转动脑筋，思考如何用程序实现上面的统计。为了简化，以字典形式表示考试成绩记录，例如：`{"zhangsan":90, "lisi":78, "wangermazi":39}`，当然，也许不止这三项，可能还有，每个老师所处理的内容稍有不同，因此字典里的键值对也不一样。

怎么做？

有几种可能要考虑到：

- 最高分或者最低分，可能有人并列。
- 要实现不同长度的字典作为输入值。
- 输出结果中，除了平均分，其它的都要有姓名和分数两项，否则都匿名了，怎么刺激学渣，表扬学霸呢？

不管你是学渣还是学霸，都能学好 Python。请思考后敲代码调试你的程序，调试之后再阅读下文。

参考代码：

    #!/usr/bin/env Python
    # coding=utf-8
    """
    统计考试成绩
    """
    from __future__ import division

    def average_score(scores):
        """
        统计平均分.
        """
        score_values = scores.values()
        sum_scores = sum(score_values)
        average = sum_scores/len(score_values)
        return average

    def sorted_score(scores):
        """
        对成绩从高到低排队.
        """
        score_lst = [(scores[k],k) for k in scores]
        sort_lst = sorted(score_lst, reverse=True)
        return [(i[1], i[0]) for i in sort_lst]

    def max_score(scores):
        """
        成绩最高的姓名和分数.
        """
        lst = sorted_score(scores)    #引用分数排序的函数 sorted_score
        max_score = lst[0][1]
        return [(i[0],i[1]) for i in lst if i[1]==max_score]

    def min_score(scores):
        """
        成绩最低的姓名和分数.
        """
        lst = sorted_score(scores)
        min_score = lst[len(lst)-1][1]
        return [(i[0],i[1]) for i in lst if i[1]==min_score]

    if __name__ == "__main__":
        examine_scores = {"google":98, "facebook":99, "baidu":52, "alibaba":80, "yahoo":49, "IBM":70, "android":76, "apple":99, "amazon":99}
    
        ave = average_score(examine_scores)
        print "the average score is: ",ave    #平均分

        sor = sorted_score(examine_scores)
        print "list of the scores: ",sor      #成绩表

        xueba = max_score(examine_scores)
        print "Xueba is: ",xueba              #学霸们

        xuezha = min_score(examine_scores)
        print "Xuzha is: ",xuezha             #学渣们

保存为 20502.py，然后运行：

    $ python 20502.py
    the average score is:  80.2222222222
    list of the scores:  [('facebook', 99), ('apple', 99), ('amazon', 99), ('google', 98), ('alibaba', 80), ('android', 76), ('IBM', 70), ('baidu', 52), ('yahoo', 49)]
    Xueba is:  [('facebook', 99), ('apple', 99), ('amazon', 99)]
    Xuzha is:  [('yahoo', 49)]

貌似结果还不错。不过，还有改进余地，看看现实，就感觉不怎么友好了。看官能不能优化一下？当然，里面的函数也不一定是最好的方法，你也可以修改优化。期盼能够在我上面公布的途径中交流一二。

## 找素数

这是一个比较常见的题目。我们姑且将范围缩小一下，找出 100 以内的素数吧。

还是按照前面的管理，读者先做，然后我提供参考代码，然后自行优化。

>質數（Prime number），又称素数，指在大於1的自然数中，除了 1 和此整数自身外，無法被其他自然数整除的数（也可定義為只有 1 和本身两个因数的数）。

>哥德巴赫猜想是数论中存在最久的未解问题之一。这个猜想最早出现在 1742 年普鲁士人克里斯蒂安·哥德巴赫与瑞士数学家莱昂哈德·欧拉的通信中。用现代的数学语言，哥德巴赫猜想可以陈述为：“任一大于 2 的偶数，都可表示成两个质数之和。”。哥德巴赫猜想在提出后的很长一段时间内毫无进展，直到二十世纪二十年代，数学家从组合数学与解析数论两方面分别提出了解决的思路，并在其后的半个世纪里取得了一系列突破。目前最好的结果是陈景润在 1973 年发表的陈氏定理（也被称为“1+2”）。（源自《维基百科》）

对这个练习，我的思路是先做一个函数，用它来判断某个整数是否是素数。然后循环即可。参考代码：

    #!/usr/bin/env Python
    # coding=utf-8

    """
    寻找素数
    """

    import math

    def is_prime(n):
        """
        判断一个数是否是素数
        """
        if n <= 1:
            return False
        for i in range(2, int(math.sqrt(n) + 1)):
            if n % i == 0:
                return False
        return True

    if __name__ == "__main__":
        primes = [i for i in range(2,100) if is_prime(i)]    #从 2 开始，因为 1 显然不是质数
        print primes

代码保存后运行：

    $ python 20503.py 
    [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]

打印出了 100 以内的质数。

还是前面的观点，这个程序你或许也发现了需要进一步优化的地方，那就太好了。另外，关于判断质数的方法，还有好多种，读者可以自己创造或者网上搜索一些，拓展思路。

## 编写函数的注意事项

编写函数，在开发实践中是非常必要和常见的，一般情况，你写的函数应该是：

1. 尽量不要使用全局变量。
2. 如果参数是可变类型数据，在函数内，不要修改它。
3. 每个函数的功能和目标要单纯，不要试图一个函数做很多事情。
4. 函数的代码行数尽量少。
5. 函数的独立性越强越好，不要跟其它的外部东西产生关联。

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：函数(4)](./204.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：类(1)](./206.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。