从你接触Java开发到现在，你对Java最直观的印象是什么呢？是它宣传的 “Write once, run anywhere”，还是目前看已经有些过于形式主义的语法呢？你对于Java平台到底了解到什么程度？请你先停下来总结思考一下。

今天我要问你的问题是，谈谈你对Java平台的理解？“Java是解释执行”，这句话正确吗？

## 典型回答

Java本身是一种面向对象的语言，最显著的特性有两个方面，一是所谓的“**书写一次，到处运行**”（Write once, run anywhere），能够非常容易地获得跨平台能力；另外就是**垃圾收集**（GC, Garbage Collection），Java通过垃圾收集器（Garbage Collector）回收分配内存，大部分情况下，程序员不需要自己操心内存的分配和回收。

我们日常会接触到JRE（Java Runtime Environment）或者JDK（Java Development Kit）。 JRE，也就是Java运行环境，包含了JVM和Java类库，以及一些模块等。而JDK可以看作是JRE的一个超集，提供了更多工具，比如编译器、各种诊断工具等。

对于“Java是解释执行”这句话，这个说法不太准确。我们开发的Java的源代码，首先通过Javac编译成为字节码（bytecode），然后，在运行时，通过 Java虚拟机（JVM）内嵌的解释器将字节码转换成为最终的机器码。但是常见的JVM，比如我们大多数情况使用的Oracle JDK提供的Hotspot JVM，都提供了JIT（Just-In-Time）编译器，也就是通常所说的动态编译器，JIT能够在运行时将热点代码编译成机器码，这种情况下部分热点代码就属于**编译执行**，而不是解释执行了。

## 考点分析

其实这个问题，问得有点笼统。题目本身是非常开放的，往往考察的是多个方面，比如，基础知识理解是否很清楚；是否掌握Java平台主要模块和运行原理等。很多面试者会在这种问题上吃亏，稍微紧张了一下，不知道从何说起，就给出个很简略的回答。

对于这类笼统的问题，你需要尽量**表现出自己的思维深入并系统化，Java知识理解得也比较全面**，一定要避免让面试官觉得你是个“知其然不知其所以然”的人。毕竟明白基本组成和机制，是日常工作中进行问题诊断或者性能调优等很多事情的基础，相信没有招聘方会不喜欢“热爱学习和思考”的面试者。

即使感觉自己的回答不是非常完善，也不用担心。我个人觉得这种笼统的问题，有时候回答得稍微片面也很正常，大多数有经验的面试官，不会因为一道题就对面试者轻易地下结论。通常会尽量引导面试者，把他的真实水平展现出来，这种问题就是做个开场热身，面试官经常会根据你的回答扩展相关问题。

## 知识扩展

回归正题，对于Java平台的理解，可以从很多方面简明扼要地谈一下，例如：Java语言特性，包括泛型、Lambda等语言特性；基础类库，包括集合、IO/NIO、网络、并发、安全等基础类库。对于我们日常工作应用较多的类库，面试前可以系统化总结一下，有助于临场发挥。

或者谈谈JVM的一些基础概念和机制，比如Java的类加载机制，常用版本JDK（如JDK 8）内嵌的Class-Loader，例如Bootstrap、 Application和Extension Class-loader；类加载大致过程：加载、验证、链接、初始化（这里参考了周志明的《深入理解Java虚拟机》，非常棒的JVM上手书籍）；自定义Class-Loader等。还有垃圾收集的基本原理，最常见的垃圾收集器，如SerialGC、Parallel GC、 CMS、 G1等，对于适用于什么样的工作负载最好也心里有数。这些都是可以扩展开的领域，我会在后面的专栏对此进行更系统的介绍。

当然还有JDK包含哪些工具或者Java领域内其他工具等，如编译器、运行时环境、安全工具、诊断和监控工具等。这些基本工具是日常工作效率的保证，对于我们工作在其他语言平台上，同样有所帮助，很多都是触类旁通的。

下图是我总结的一个相对宽泛的蓝图供你参考。

![](https://static001.geekbang.org/resource/image/20/32/20bc6a900fc0b829c2f0e723df050732.png?wh=1265%2A706)

不再扩展了，回到前面问到的解释执行和编译执行的问题。有些面试官喜欢在特定问题上“刨根问底儿”，因为这是进一步了解面试者对知识掌握程度的有效方法，我稍微深入探讨一下。

众所周知，我们通常把Java分为编译期和运行时。这里说的Java的编译和C/C++是有着不同的意义的，Javac的编译，编译Java源码生成“.class”文件里面实际是字节码，而不是可以直接执行的机器码。Java通过字节码和Java虚拟机（JVM）这种跨平台的抽象，屏蔽了操作系统和硬件的细节，这也是实现“一次编译，到处执行”的基础。

在运行时，JVM会通过类加载器（Class-Loader）加载字节码，解释或者编译执行。就像我前面提到的，主流Java版本中，如JDK 8实际是解释和编译混合的一种模式，即所谓的混合模式（-Xmixed）。通常运行在server模式的JVM，会进行上万次调用以收集足够的信息进行高效的编译，client模式这个门限是1500次。Oracle Hotspot JVM内置了两个不同的JIT compiler，C1对应前面说的client模式，适用于对于启动速度敏感的应用，比如普通Java桌面应用；C2对应server模式，它的优化是为长时间运行的服务器端应用设计的。默认是采用所谓的分层编译（TieredCompilation）。这里不再展开更多JIT的细节，没必要一下子就钻进去，我会在后面介绍分层编译的内容。

Java虚拟机启动时，可以指定不同的参数对运行模式进行选择。 比如，指定“-Xint”，就是告诉JVM只进行解释执行，不对代码进行编译，这种模式抛弃了JIT可能带来的性能优势。毕竟解释器（interpreter）是逐条读入，逐条解释运行的。与其相对应的，还有一个“-Xcomp”参数，这是告诉JVM关闭解释器，不要进行解释执行，或者叫作最大优化级别。那你可能会问这种模式是不是最高效啊？简单说，还真未必。“-Xcomp”会导致JVM启动变慢非常多，同时有些JIT编译器优化方式，比如分支预测，如果不进行profiling，往往并不能进行有效优化。

除了我们日常最常见的Java使用模式，其实还有一种新的编译方式，即所谓的AOT（Ahead-of-Time Compilation），直接将字节码编译成机器代码，这样就避免了JIT预热等各方面的开销，比如Oracle JDK 9就引入了实验性的AOT特性，并且增加了新的jaotc工具。利用下面的命令把某个类或者某个模块编译成为AOT库。

```
jaotc --output libHelloWorld.so HelloWorld.class
jaotc --output libjava.base.so --module java.base
```

然后，在启动时直接指定就可以了。

```
java -XX:AOTLibrary=./libHelloWorld.so,./libjava.base.so HelloWorld
```

而且，Oracle JDK支持分层编译和AOT协作使用，这两者并不是二选一的关系。如果你有兴趣，可以参考相关文档：[http://openjdk.java.net/jeps/295](http://openjdk.java.net/jeps/295)。AOT也不仅仅是只有这一种方式，业界早就有第三方工具（如GCJ、Excelsior JET）提供相关功能。

另外，JVM作为一个强大的平台，不仅仅只有Java语言可以运行在JVM上，本质上合规的字节码都可以运行，Java语言自身也为此提供了便利，我们可以看到类似Clojure、Scala、Groovy、JRuby、Jython等大量JVM语言，活跃在不同的场景。

今天，我简单介绍了一下Java平台相关的一些内容，目的是提纲挈领地构建一个整体的印象，包括Java语言特性、 核心类库与常用第三方类库、Java虚拟机基本原理和相关工具，希望对你有所帮助。

## 一课一练

关于今天我们讨论的题目你做到心中有数了吗？知道不如做到，请你也在留言区写写自己对Java平台的理解。我会选出经过认真思考的留言，送给你一份学习鼓励金，欢迎你与我一起讨论。

你的朋友是不是也在准备面试呢？你可以“请朋友读”，把今天的题目分享给好友，或许你能帮到他。
<div><strong>精选留言（15）</strong></div><ul>
<li><span>Woj</span> 👍（1065） 💬（19）<p>        “一次编译、到处运行”说的是Java语言跨平台的特性，Java的跨平台特性与Java虚拟机的存在密不可分，可在不同的环境中运行。比如说Windows平台和Linux平台都有相应的JDK，安装好JDK后也就有了Java语言的运行环境。其实Java语言本身与其他的编程语言没有特别大的差异，并不是说Java语言可以跨平台，而是在不同的平台都有可以让Java语言运行的环境而已，所以才有了Java一次编译，到处运行这样的效果。
        严格的讲，跨平台的语言不止Java一种，但Java是较为成熟的一种。“一次编译，到处运行”这种效果跟编译器有关。编程语言的处理需要编译器和解释器。Java虚拟机和DOS类似，相当于一个供程序运行的平台。
        程序从源代码到运行的三个阶段：编码——编译——运行——调试。Java在编译阶段则体现了跨平台的特点。编译过程大概是这样的：首先是将Java源代码转化成.CLASS文件字节码，这是第一次编译。.class文件就是可以到处运行的文件。然后Java字节码会被转化为目标机器代码，这是是由JVM来执行的，即Java的第二次编译。
        “到处运行”的关键和前提就是JVM。因为在第二次编译中JVM起着关键作用。在可以运行Java虚拟机的地方都内含着一个JVM操作系统。从而使JAVA提供了各种不同平台上的虚拟机制，因此实现了“到处运行”的效果。需要强调的一点是，java并不是编译机制，而是解释机制。Java字节码的设计充分考虑了JIT这一即时编译方式，可以将字节码直接转化成高性能的本地机器码，这同样是虚拟机的一个构成部分。</p>2018-05-05</li><br/><li><span>magict4</span> 👍（611） 💬（14）<p>我对『Compile once, run anywhere』这个宣传语提出的历史背景非常感兴趣。这个宣传语似乎在暗示 C 语言有一个缺点：对于每一个不同的平台，源代码都要被编译一次。我不解的地方是，为什么这会是一个问题？不同的平台，可执行的机器码必然是不一样的。源代码自然需要依据不同的平台分别被编译。 我觉得真正问题不在编译这一块，而是在 C 语言源文件这一块。我没有 C 语言的编程经验，但是似乎 C 语言程序经常需要调用操作系统层面的 API。不同的操作系统，API 一般不同。为了支持多平台，C 语言程序的源文件需要根据不同平台修改多次。这应该是一个非常大的痛点。我回头查了一下当时的宣传语，原文是『Write once, run anywhere』，焦点似乎并不在编译上，而是在对源文件的修改上。

以上是自己一点不成熟的想法，还请大家指正！</p>2018-05-05</li><br/><li><span>三军</span> 👍（467） 💬（5）<p>Java特性:
面向对象（封装，继承，多态）
平台无关性（JVM运行.class文件）
语言（泛型，Lambda）
类库（集合，并发，网络，IO&#47;NIO）
JRE（Java运行环境，JVM，类库）
JDK（Java开发工具，包括JRE，javac，诊断工具）

Java是解析运行吗？
不正确！
1，Java源代码经过Javac编译成.class文件
2，.class文件经JVM解析或编译运行。
（1）解析:.class文件经过JVM内嵌的解析器解析执行。
（2）编译:存在JIT编译器（Just In Time Compile 即时编译器）把经常运行的代码作为&quot;热点代码&quot;编译与本地平台相关的机器码，并进行各种层次的优化。
（3）AOT编译器: Java 9提供的直接将所有代码编译成机器码执行。</p>2018-05-05</li><br/><li><span>Jerry银银</span> 👍（262） 💬（11）<p>关注了好久，终于期盼到了第一讲。

在看到这个题目时，我并没有立马点进来看原文，而是给了自己一些时间进行思考。

首先，个人觉得这个题目非常的抽象和笼统，这个问题没有标准答案，但是有『好』答案，而答案的好坏，完全取决于面试者自身的技术素养和对Java系统性的了解。我的理解如下：

宏观角度：
跟c&#47;c++最大的不同点在于，c&#47;c++编程是面向操作系统的，需要开发者极大地关心不同操作系统之间的差异性；而Java平台通过虚拟机屏蔽了操作系统的底层细节，使得开发者无需过多地关心不同操作系统之间的差异性。
通过增加一个间接的中间层来进行”解耦“是计算机领域非常常用的一种”艺术手法“，虚拟机是这样，操作系统是这样，HTTP也是这样。

Java平台已经形成了一个生态系统，在这个生态系统中，有着诸多的研究领域和应用领域：
1. 虚拟机、编译技术的研究(例如：GC优化、JIT、AOT等)：对效率的追求是人类的另一个天性之一
2. Java语言本身的优化
3. 大数据处理
4. Java并发编程
5. 客户端开发（例如：Android平台）
6. ......


微观角度：
Java平台中有两大核心：
1. Java语言本身、JDK中所提供的核心类库和相关工具
2. Java虚拟机以及其他包含的GC

1. Java语言本身、JDK中所提供的核心类库和相关工具
从事Java平台的开发，掌握Java语言、核心类库以及相关工具是必须的，我觉得这是基础中的基础。
&gt;&gt; 对语言本身的了解，需要开发者非常熟悉语言的语法结构；而Java又是一种面对对象的语言，这又需要开发者深入了解面对对象的设计理念；
&gt;&gt; Java核心类库包含集合类、线程相关类、IO、NIO、J.U.C并发包等；	
&gt;&gt; JDK提供的工具包含：基本的编译工具、虚拟机性能检测相关工具等。

2. Java虚拟机
Java语言具有跨平台的特性，也正是因为虚拟机的存在。Java源文件被编译成字节码，被虚拟机加载后执行。这里隐含的意思有两层：
1）大部分情况下，编程者只需要关心Java语言本身，而无需特意关心底层细节。包括对内存的分配和回收，也全权交给了GC。
2）对于虚拟机而言，只要是符合规范的字节码，它们都能被加载执行，当然，能正常运行的程序光满足这点是不行的，程序本身需要保证在运行时不出现异常。所以，Scala、Kotlin、Jython等语言也可以跑在虚拟机上。

围绕虚拟机的效率问题展开，将涉及到一些优化技术，例如：JIT、AOT。因为如果虚拟机加载字节码后，完全进行解释执行，这势必会影响执行效率。所以，对于这个运行环节，虚拟机会进行一些优化处理，例如JIT技术，会将某些运行特别频繁的代码编译成机器码。而AOT技术，是在运行前，通过工具直接将字节码转换为机器码。</p>2018-05-06</li><br/><li><span>姜亮</span> 👍（186） 💬（5）<p>写个程序直接执行字节码就是解释执行。写个程序运行时把字节码动态翻译成机器码就是jit。写个程序把java源代码直接翻译为机器码就是aot。造个CPU直接执行字节码，字节码就是机器码。</p>2018-05-07</li><br/><li><span>欧阳田</span> 👍（158） 💬（6）<p>1，JVM的内存模型，堆、栈、方法区；字节码的跨平台性；对象在JVM中的强引用，弱引用，软引用，虚引用，是否可用finalise方法救救它？；双亲委派进行类加载，什么是双亲呢？双亲就是多亲，一份文档由我加载，然后你也加载，这份文档在JVM中是一样的吗？；多态思想是Java需要最核心的概念，也是面向对象的行为的一个最好诠释；理解方法重载与重写在内存中的执行流程，怎么定位到这个具体方法的。2，发展流程，JDK5(重写bug)，JDK6(商用最稳定版)，JDK7(switch的字符串支持)，JDK8(函数式编程)，一直在发展进化。3，理解祖先类Object，它的行为是怎样与现实生活连接起来的。4，理解23种设计模式，因为它是道与术的结合体。</p>2018-05-05</li><br/><li><span>zaiweiwoaini</span> 👍（130） 💬（1）<p>看评论也能学习知识。 </p>2018-05-05</li><br/><li><span>刻苦滴涛涛</span> 👍（101） 💬（5）<p>我理解的java程序执行步骤:
首先javac编译器将源代码编译成字节码。
然后jvm类加载器加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度相对会比较慢。有些方法和代码块是高频率调用的，也就是所谓的热点代码，所以引进jit技术，提前将这类字节码直接编译成本地机器码。这样类似于缓存技术，运行时再遇到这类代码直接可以执行，而不是先解释后执行。</p>2018-05-05</li><br/><li><span>thinkers</span> 👍（99） 💬（4）<p>jre为java提供了必要的运行时环境，jdk为java提供了必要的开发环境！</p>2018-05-05</li><br/><li><span>scott</span> 👍（86） 💬（3）<p>解释执行和编译执行有何区别</p>2018-05-07</li><br/><li><span>Geek_zbvt62</span> 👍（56） 💬（3）<p>这种基于运行分析，进行热点代码编译的设计，是因为绝大多数的程序都表现为“小部分的热点耗费了大多数的资源”吧。只有这样才能做到，在某些场景下，一个需要跑在运行时上的语言，可以比直接编译成机器码的语言更“快”</p>2018-05-05</li><br/><li><span>一叶追寻</span> 👍（41） 💬（1）<p>对Java平台的理解，首先想到的是Java的一些特性，比如平台无关性、面向对象、GC机制等，然后会在这几个方面去回答。平台无关性依赖于JVM，将.class文件解释为适用于操作系统的机器码。面向对象则会从封装、继承、多态这些特性去解释，具体内容就不在评论里赘述了。另外Java的内存回收机制，则涉及到Java的内存结构，堆、栈、方法区等，然后围绕什么样的对象可以回收以及回收的执行。以上是我对本道题的理解，不足之处还请杨老师指出，希望通过这次学习能把Java系统的总结一下~</p>2018-05-05</li><br/><li><span>石头狮子</span> 👍（36） 💬（2）<p>1. 一次编译，到处运行。jvm 层面封装了系统API，提供不同系统一致的调用行为。减少了为适配不同操作系统，不同架构的带来的工作量。
2. 垃圾回收，降低了开发过程中需要注意内存回收的难度。降低内存泄露出现的概率。虽然也带来了一些额外开销，但是足以弥补带来的好处。合理的分代策略，提高了内存使用率。
3. jit 与其他编译语言相比，降低了编译时间，因为大部分代码是运行时编译，避免了冷代码在编译时也参与编译的问题。
    提高了代码的执行效率，之前项目中使用过 lua 进行相关开发。由于 lua 是解释性语言，并配合使用了 lua-jit。开发过程中遇到，如果编写的 lua 代码是 jit 所不支持的会导致代码性能与可编译的相比十分低下。
</p>2018-05-05</li><br/><li><span>櫻の空</span> 👍（32） 💬（3）<p>以下是我在本节课所得到的收获，结合TIJ的内容整理了一下我个人的理解，若有错误，还望老师指出。
Java采用的是解释和编译混合的模式。它首先通过javac将源码编译成字节码文件class.然后在运行的时候通过解释器或者JIT将字节码转换成最终的机器码。
只是用解释器的缺点：抛弃了JIT可能带来的性能优势。如果代码没有被JIT编译的话，再次运行时需要重复解析。
只用JIT的缺点：
需要将全部的代码编译成本地机器码。要花更多的时间，JVM启动会变慢非常多；
增加可执行代码的长度（字节码比JIT编译后的机器码小很多），这将导致页面调度，从而降低程序的速度。
有些JIT编译器的优化方式，比如分支预测，如果不进行profiling，往往并不能进行有效优化。
因此，HotSpot采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（热点代码），而这也就是JIT所需要编译的部分。JVM会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度就越快。
JDK 9引入了一种新的编译模式AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了JIT预热等各方面的开销。JDK支持分层编译和AOT协作使用。
注：JIT为方法级，它会缓存编译过的字节码在CodeCache中，而不需要被重复解释</p>2018-05-14</li><br/><li><span>Dee1024</span> 👍（24） 💬（1）<p>传统Java是解释型的语言，现在的JIT、AOT，让Java也支持了编译型语言的特性；
传统Java是面向对象的语言，JDK8引入Lambda，让Java也有了函数式编程的能力；
传统的Java是命令式编程范式，JDK9引入Flow，让Java更好的支持响应式编程范式；
... ...

Java是一个成熟稳定的语言和平台，更是历久弥新语言。
</p>2018-09-13</li><br/>
</ul>