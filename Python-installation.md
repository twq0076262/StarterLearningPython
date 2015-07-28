# Python 安装

任何高级语言都是需要一个自己的编程环境的，这就好比写字一样，需要有纸和笔，在计算机上写东西，也需要有文字处理软件，比如各种名称的 OFFICE。笔和纸以及 office 软件，就是写东西的硬件或软件，总之，那些文字只能写在那个上边，才能最后成为一篇文章。那么编程也是，要有个什么程序之类的东西，要把程序写到那个上面，才能形成最后类似文章那样的东西。

>**注：推荐一种非常重要的学习方法**

>在我这里看文章的零基础朋友，乃至于非零基础的朋友，不要希望在这里学到很多高深的 Python 语言技巧。

>“靠，那看你胡扯吗？”

>非也。重要的是学会一些方法。比如刚才给大家推荐的“上网 google 一下”，就是非常好的学习方法。互联网的伟大之处，不仅仅在于打打游戏、看看养眼的照片或者各种视频之类的，当然，在某国很长时间互联网等于娱乐网，我忠心希望从读本文的朋友开始，互联网不仅仅是娱乐网，还是知识网和创造网。扯远了，拉回来。在学习过程中，如果遇到一点点疑问，都不要放过，思考一下、尝试一下之后，不管有没有结果，还都要 google 一下。

>列位看好了，我上面写的很清楚，是 google 一下，不是让大家去用那个什么度来搜索，那个搜索是专用搜索八卦、假药、以及各种穿着很简单衣服的女孩子照片的。如果你真的要提高自己的技术视野并且专心研究技术问题，请用 google。当然，我知道你在用的时候会遇到困难，做为一个要在技术上有点成就的人，一定要学点上网的技术的，你懂得。

>什么？你不懂？你的确是我的读者：零基础。那就具体来问我吧，不管是加入 ＱＱ 群还是微博，都可以。

欲练神功，挥刀自宫。神功是有前提的。

要学 Python，不用自宫。Python 不用那么残忍的前提，但是，也需要安装点东西才能用。

所需要安装的东西，都在这个页面里面：[www.Python.org/downloads/](www.Python.org/downloads/)

>[www.python.org](www.python.org)是 python 的官方网站，如果你的英语足够使用，那么自己在这里阅读，可以获得非常多的收获。

在 Python 的下载页面里面，显示出 Python 目前有两大类，一类是 Python3.x.x，另外一类是 Python2.7.x。可以说，Python3 是未来，它比 Python2.7 有进步。但是，现在，还有很多东西没有完全兼容 Python3。更何况，如果学了 Python2.7，对于 Python3，也只是某些地方的小变化了。

所以，我这里是用 Python2.7 为例子来讲授的。

## Linux 系统的安装

你的计算机是什么操作系统的？自己先弄懂。如果是 Linux 某个发行版，就跟我同道了。并且我恭喜你，因为以后会安装更多的一些 Python 库（模块），在这种操作系统下，操作非常简单，当然，如果是 iOS，也一样，因为都是 UNIX 下的蛋。只是 widows 有点另类了。

不过，没关系，Python 就是跨平台的。

但是，我还是推荐列位，至少在某种意义上讲，用 Linux 操作系统是很好的事情。

我用 Ubuntu。

以 ubutu14.04 为例，一般只要装好了这个操作系统，里面就已经把 Python 安装好了。可能是 Python2.7.6 版本，不过，在我来看，不需要升级，虽然目前最高版本是 Python2.7.9（在 64 位的上面，默认也安装了 Python3，供使用者选择）。

接下来就在 shell 中输入 Python，如果看到了`>>>`，并且显示出 Python 的版本信息，恭喜你，这就进入到了 Python 的交互模式下。

如果非要自己安装。参考下面的操作：

- 到官方网站下载源码。比如：
    
    wget <http://www.python.org/ftp/python/2.7.8/Python-2.7.8.tgz>
    
- 解压源码包
    
    tar -zxvf Python-2.7.8.tgz
    
- 编译
    
    cd Python-2.7.8
    ./configure  --prefix=/usr/local    # 指定了目录，如果不制定，可以使用默认的，直接运行 ./configure     即可。
    make&&sudo make install

安装好之后，进入 shell，输入 Python，会看到如下：

    qw@qw-Latitude-E4300:~$ python
    Python 2.7.6 (default, Nov 13 2013, 19:24:16)   # 后来我升级到 2.7.8 了,就是用后面讲到的源码安装方法
    [GCC 4.6.3] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> 

我用的是 Python2.7.6，或许你的版本号更高。这些差别就不用纠结了。

## windows 系统的安装

到[下载页面里面](https://www.python.org/download/releases/2.7.8/)找到 windows 安装包，下载之，比如下载了这个文件：Python-2.7.8.msi。然后就是不断的“下一步”，即可完成安装。

特别注意，安装完之后，需要检查一下，在环境变量是否有 Python。

>如果还不知道什么是 windows 环境变量，以及如何设置。不用担心，请 google 一下，搜索："windows 环境变量"就能找到如何设置了。

以上搞定，在 cmd 中，输入 Python，得到跟上面类似的结果，就说明已经安装好了。

## Mac OS X 系统的安装

其实根本就不用再写怎么安装了，因为用 Mac OS X 的朋友，肯定是高手中的高高手了，至少我一直很敬佩那些用 Mac OS X 并坚持没有更换为 windows 的。麻烦用 Mac OS X 的朋友自己网上搜吧，跟前面 unbutu 差不多。

如果按照以上方法，顺利安装成功，只能说明幸运，无它。如果没有安装成功，这是提高自己的绝佳机会，因为只有遇到问题才能解决问题，才能知道更深刻的道理，不要怕，有 google，它能帮助列为看官解决所有问题。当然，加入 ＱＱ 群或者通过微博，问我也可以。

就一般情况而言，Linux 和 Mac OS x 系统都已经安装了某种 Python 的版本，打开就可以使用。但是 windows 是肯定不安装的。除了可以用上面所说的方法安装，还有一个更省事的方法，就是安装：ActivePython

简单记录一下我的安装方法（我是在 linux 系统中做的）：

1. 获得 root 权限
2. 到上述地址下载某种版本的 Python: wget <https://www.Python.org/ftp/Python/2.7.8/Python-2.7.8.tgz>
3. 解压缩：tar xfz Python-2.7.8.tgz
4. 进入该目录：cd Python-2.7.8
5. 配置： ./configure
6. 在上述文件夹内运行：make，然后运行：make install
7. 祝你幸运
8. 安装完毕

OK!已经安装好之后，马上就可以开始编程了。

最后喊一句在一个编程视频课程广告里面看到的口号，很有启发：“我们程序员，不求通过，但求报错”。

还需要补充说明，本教程使用的是 Python2，虽然跟 Python3 有区别，但是，你不用纠结是 2 还是 3，因为两者区别不是很大，再者，目前工程上应用最多的，还是 Python2，虽然 Python3 是趋势，毕竟需要时间过渡的。很多初学者特别是大学生喜欢纠缠这个问题，实在有点浪费脑细胞了。

-------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：从小工到专家](./02.md)|&nbsp;&nbsp;&nbsp;[下节：集成开发环境](./101.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。