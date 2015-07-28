# 类(1)

类，这个词如果是你第一次听到，把它作为一个单独的名词，总感觉怪怪的，因为在汉语体系中，很常见的是说“鸟类”、“人类”等词语，而单独说“类”，总感觉前面缺点修饰成分。其实，它对应的是英文单词 class，“类”是这个 class 翻译过来的，你就把它作为一个翻译术语吧。

除了“类”这个术语，从现在开始，还要经常提到一个 OOP，即面向对象编程（或者“面向对象程序设计”）。

为了理解类和 OOP，需要对一些枯燥的名词有了解。

## 术语

必须了解这些术语的基本含义，因为后面经常用到。下面的术语定义均来自维基百科。

### 问题空间

**定义：**

>问题空间是问题解决者对一个问题所达到的全部认识状态，它是由问题解决者利用问题所包含的信息和已贮存的信息主动地构成的。

一个问题一般有下面三个方面来定义：

- 初始状态——一开始时的不完全的信息或令人不满意的状况；
- 目标状态——你希望获得的信息或状态；
- 操作——为了从初始状态迈向目标状态，你可能采取的步骤。

这三个部分加在一起定义了问题空间（problem space）。

### 对象

**定义：**

>对象（object），台湾译作物件，是面向对象（Object Oriented）中的术语，既表示客观世界问题空间（Namespace）中的某个具体的事物，又表示软件系统解空间中的基本元素。

把 object 翻译为“对象”，是比较抽象的。因此，有人认为，不如翻译为“物件”更好。因为“物件”让人感到一种具体的东西。

这种看法在某些语言中是非常适合的。但是，在 Python 中，则无所谓，不管怎样，Python 中的一切都是对象，不管是字符串、函数、模块还是类，都是对象。“万物皆对象”。

都是对象有什么优势吗？太有了。这说明 Python 天生就是 OOP 的。也说明，Python 中的所有东西，都能够进行拼凑组合应用，因为对象就是可以拼凑组合应用的。

对于对象这个东西，OOP 大师 Grandy Booch 的定义，应该是权威的，相关定义的内容包括：

- **对象**：一个对象有自己的状态、行为和唯一的标识；所有相同类型的对象所具有的结构和行为在他们共同的类中被定义。
- **状态（state）**：包括这个对象已有的属性（通常是类里面已经定义好的）在加上对象具有的当前属性值（这些属性往往是动态的）
- **行为（behavior）**：是指一个对象如何影响外界及被外界影响，表现为对象自身状态的改变和信息的传递。
- **标识（identity）**：是指一个对象所具有的区别于所有其它对象的属性。（本质上指内存中所创建的对象的地址）

大师的话的确有水平，听起来非常高深。不过，初学者可能理解起来就有点麻烦了。我就把大师的话化简一下，但是化简了之后可能在严谨性上就不足了，我想对于初学者来讲，应该是影响不很大的。随着学习和时间的深入，就更能理解大师的严谨描述了。

简化之，对象应该具有属性（就是上面的状态，因为属性更常用）、方法（就是上面的行为，方法跟常被使用）和标识。因为标识是内存中自动完成的，所以，平时不用怎么管理它。主要就是属性和方法。

为了体现“深入浅出”的道理，还是讲故事吧。

既然万物都是对象，那么，某个具体的人也是对象，这是当然的事情。假设这个具体的人就是德艺双馨的苍老师，她是一个对象。这个苍老师具有哪些特征呢？我错了，写到这里发现不能用苍老师为对象的例子，因为容易让读者不专心学习了。我换一个吧，以某个王美女为对象说明（这个王美女完全是虚构的，请不要对号入座，更不要想入非非，如果雷同，纯属巧合）。

王美女这个对象具有某些特征，眼睛，大；腿，长；皮肤，白。当然，既然是美女，肯定还有别的显明特征，读者可以自己假设去。如果用“对象”的术语来说明，就说这些特征都是她的属性。也就是说**属性是一个对象做具有的特征，或曰：是什么。**。

王美女除了具有上面的特征之外，她还能做一些事情，比如她能唱歌、会吹拉弹唱等。这些都是她能够做的事情。用“对象”的术语来说，就是她的“方法”。即**方法就是对象能够做什么**。

任何一个对象都要包括这两部分：属性（是什么）和方法（能做什么）。

### 面向对象

**定义：**

>面向对象程序设计（英语：Object-oriented programming，缩写：OOP）是一种程序设计范型，同时也是一种程序开发的方法。对象指的是类的实例。它将对象作为程序的基本单元，将程序和数据封装其中，以提高软件的重用性、灵活性和扩展性。

>面向对象程序设计可以看作一种在程序中包含各种独立而又互相调用的对象的思想，这与传统的思想刚好相反：传统的程序设计主张将程序看作一系列函数的集合，或者直接就是一系列对电脑下达的指令。面向对象程序设计中的每一个对象都应该能够接受数据、处理数据并将数据传达给其它对象，因此它们都可以被看作一个小型的“机器”，即对象。

>目前已经被证实的是，面向对象程序设计推广了程序的灵活性和可维护性，并且在大型项目设计中广为应用。 此外，支持者声称面向对象程序设计要比以往的做法更加便于学习，因为它能够让人们更简单地设计并维护程序，使得程序更加便于分析、设计、理解。反对者在某些领域对此予以否认。

>当我们提到面向对象的时候，它不仅指一种程序设计方法。它更多意义上是一种程序开发方式。在这一方面，我们必须了解更多关于面向对象系统分析和面向对象设计（Object Oriented Design，简称 OOD）方面的知识。

下面再引用一段来自维基百科中关于 OOP 的历史。

>面向对象程序设计的雏形，早在 1960 年的 Simula 语言中即可发现，当时的程序设计领域正面临着一种危机：在软硬件环境逐渐复杂的情况下，软件如何得到良好的维护？面向对象程序设计在某种程度上通过强调可重复性解决了这一问题。20 世纪 70 年代的 Smalltalk 语言在面向对象方面堪称经典——以至于 30 年后的今天依然将这一语言视为面向对象语言的基础。

>计算机科学中对象和实例概念的最早萌芽可以追溯到麻省理工学院的 PDP-1 系统。这一系统大概是最早的基于容量架构（capability based architecture）的实际系统。另外 1963 年 Ivan Sutherland 的 Sketchpad 应用中也蕴含了同样的思想。对象作为编程实体最早是于 1960 年代由 Simula 67 语言引入思维。Simula 这一语言是奥利-约翰·达尔和克利斯登·奈加特在挪威奥斯陆计算机中心为模拟环境而设计的。（据说，他们是为了模拟船只而设计的这种语言，并且对不同船只间属性的相互影响感兴趣。他们将不同的船只归纳为不同的类，而每一个对象，基于它的类，可以定义它自己的属性和行为。）这种办法是分析式程序的最早概念体现。在分析式程序中，我们将真实世界的对象映射到抽象的对象，这叫做“模拟”。Simula 不仅引入了“类”的概念，还应用了实例这一思想——这可能是这些概念的最早应用。
 
>20 世纪 70 年代施乐 PARC 研究所发明的 Smalltalk 语言将面向对象程序设计的概念定义为，在基础运算中，对对象和消息的广泛应用。Smalltalk 的创建者深受 Simula 67 的主要思想影响，但 Smalltalk 中的对象是完全动态的——它们可以被创建、修改并销毁，这与 Simula 中的静态对象有所区别。此外，Smalltalk 还引入了继承性的思想，它因此一举超越了不可创建实例的程序设计模型和不具备继承性的 Simula。此外，Simula 67 的思想亦被应用在许多不同的语言，如 Lisp、Pascal。

>面向对象程序设计在 80 年代成为了一种主导思想，这主要应归功于 C++——C 语言的扩充版。在图形用户界面（GUI）日渐崛起的情况下，面向对象程序设计很好地适应了潮流。GUI 和面向对象程序设计的紧密关联在 Mac OS X 中可见一斑。Mac OS X 是由 Objective-C 语言写成的，这一语言是一个仿 Smalltalk 的 C 语言扩充版。面向对象程序设计的思想也使事件处理式的程序设计更加广泛被应用（虽然这一概念并非仅存在于面向对象程序设计）。一种说法是，GUI 的引入极大地推动了面向对象程序设计的发展。

>苏黎世联邦理工学院的尼克劳斯·维尔特和他的同事们对抽象数据和模块化程序设计进行了研究。Modula-2 将这些都包括了进去，而 Oberon 则包括了一种特殊的面向对象方法——不同于 Smalltalk 与 C++。

>面向对象的特性也被加入了当时较为流行的语言：Ada、BASIC、Lisp、Fortran、Pascal 以及种种。由于这些语言最初并没有面向对象的设计，故而这种糅合常常会导致兼容性和维护性的问题。与之相反的是，“纯正的”面向对象语言却缺乏一些程序员们赖以生存的特性。在这一大环境下，开发新的语言成为了当务之急。作为先行者，Eiffel 成功地解决了这些问题，并成为了当时较受欢迎的语言。

>在过去的几年中，Java 语言成为了广为应用的语言，除了它与 C 和 C++ 语法上的近似性。Java 的可移植性是它的成功中不可磨灭的一步，因为这一特性，已吸引了庞大的程序员群的投入。

>在最近的计算机语言发展中，一些既支持面向对象程序设计，又支持面向过程程序设计的语言悄然浮出水面。它们中的佼佼者有 Python、Ruby 等等。

>正如面向过程程序设计使得结构化程序设计的技术得以提升，现代的面向对象程序设计方法使得对设计模式的用途、契约式设计和建模语言（如 UML）技术也得到了一定提升。

列位看官，当您阅读到这句话的时候，我就姑且认为您已经对面向对象有了一个模糊的认识了。那么，类和 OOP 有什么关系呢？

### 类

**定义：**

>在面向对象程式设计，类（class）是一种面向对象计算机编程语言的构造，是创建对象的蓝图，描述了所创建的对象共同的属性和方法。

>类的更严格的定义是由某种特定的元数据所组成的内聚的包。它描述了一些对象的行为规则，而这些对象就被称为该类的实例。类有接口和结构。接口描述了如何通过方法与类及其实例互操作，而结构描述了一个实例中数据如何划分为多个属性。类是与某个层的对象的最具体的类型。类还可以有运行时表示形式（元对象），它为操作与类相关的元数据提供了运行时支持。

>支持类的编程语言在支持与类相关的各种特性方面都多多少少有一些微妙的差异。大多数都支持不同形式的类继承。许多语言还支持提供封装性的特性，比如访问修饰符。类的出现，为面向对象编程的三个最重要的特性（封装性，继承性，多态性），提供了实现的手段。

看到这里，看官或许有一个认识，要 OOP 编程，就得用到类。可以这么说，虽然不是很严格。但是，反过来就不能说了。不是说用了类就一定是 OOP。

## 编写类

首先要明确，类是对某一群具有同样属性和方法的对象的抽象。比如这个世界上有很多长翅膀并且会飞的生物，于是聪明的人们就将它们统一称为“鸟”——这就是一个类，虽然它也可以称作“鸟类”。

还是以美女为例子，因为这个例子不仅能阅读本课程不犯困，还能兴趣昂然。

要定义类，就要抽象，找出共同的方面。

    class 美女:        #用 class 来声明，后面定义的是一个类
        pass

好，现在就从这里开始，编写一个类，不过这次我们暂时不用 Python，而是用伪代码，当然，这个代码跟 Python 相去甚远。如下：

    class 美女:
        胸围 = 90
        腰围 = 58
        臀围 = 83
        皮肤 = white
        唱歌()
        做饭()

定义了一个名称为“美女”的类，其中我约定，没有括号的是属性，带有括号的是方法。这个类仅仅是对美女的通常抽象，并不是某个具体美女.

对于一个具体的美女，比如前面提到的苍老师或者王美女，她们都是上面所定义的“美女”那个类的具体化，这在编程中称为“美女类”的实例。

    王美女 = 美女()
    
我用这样一种表达方式，就是将“美女类”实例化了，对“王美女”这个实例，就可以具体化一些属性，比如胸围；还可以具体实施一些方法，比如做饭。通常可以用这样一种方式表示：

    a = 王美女.胸围
    
用点号`.`的方式，表示王美女胸围的属性，得到的变量 a 就是 90.另外，还可以通过这种方式给属性赋值，比如

    王美女.皮肤 = black
    
这样，这个实例（王美女）的皮肤就是黑色的了。

通过实例，也可以访问某个方法，比如：

    王美女.做饭()
    
这就是在执行一个方法，让王美女这个实例做饭。现在也比较好理解了，只有一个具体的实例才能做饭。

至此，你是否对类和实例，类的属性和方法有初步理解了呢？

------

[总目录](./index.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[上节：函数练习](./205.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[下节：类(2)](./207.md)

如果你认为有必要打赏我，请通过支付宝：**qiwsir@126.com**,不胜感激。