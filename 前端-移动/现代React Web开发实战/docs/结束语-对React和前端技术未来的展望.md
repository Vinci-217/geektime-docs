你好，我是宋一玮。

时间过得真快，从5月底《现代React Web开发实战》专栏开始立项，8月下旬开始连载，转眼就到10月下旬连载结束了。

这里我想先重提一下我在[开篇词](https://time.geekbang.org/column/article/555109?)中对你的期望：**学习一门技术，务必要有大于一门技术的收获**。

之所以有这个初衷，是因为我从业16年，深刻理解到，软件开发的从业者需要具有终身学习的能力和决心。然而随着离开学校步入职场，之后再经历过职业或人生的一些重要阶段，我们可以用于学习的时间和精力只会越来越少、越来越碎片化。

不论是追逐理想还是直面功利，学习新技术时都值得多花些心思：如何用有限的学习换来更多的收获。

这个专栏整体都是按照这个初衷设计的。如果回头翻翻目录你会发现：

- 历史篇在复习（了解）前端开发技术历史的同时，尝试用你可能已经熟悉的知识引出React；
- “独狼”篇一开始，通过一个简单的看板项目为你演示如何开发React应用，然后抽丝剥茧，一边讲解React中的概念和API，一边介绍背后的前端领域知识；
- 项目篇则是选出大中型React项目中会遇到的典型挑战，跳出React技术分析这些挑战的本质，然后再回到React中解决它们。

不知你经过这个专栏的学习，是否有比React技术本身更多的收获呢？

## 前端技术的变与不变

专栏的[第1节课](https://time.geekbang.org/column/article/553789)，曾用Java Web技术与包括React在内的现代JS Web技术做对比，讨论了前端技术的变与不变。这里我不打算再反复强调哪些技术点会变，哪些不会变。而是换个角度，聊聊前端开发者。

如今网络上的信息极为丰富，甚至是过载的。只要简单搜索，你就可以得到很多既成的结论，比如新技术A就是老技术M的马甲，新技术B就是老技术X、Y、Z的缝合，新技术C刚推出就过时了等等。

这些可以信，但不建议尽信。快速了解技术的变与不变，多少可以走些捷径，但如果一个开发者所有的判断都来自二手或三手资料，那这些判断只会越来越虚。

陆游说得好：

> 纸上得来终觉浅，绝知此事要躬行。

一位经验丰富的前端开发者并不等于优秀的前端开发者，但任何组织任何人都不应该否定经验的价值。**经验不仅代表过去，更可以支撑起一个可预期的未来**（这样说主要还是为35岁以上的开发者正名）。年轻的同学们也不妨戒骄戒躁，攒经验本来也是一个**量变到质变**的过程，你今天学过的、做过的，都会成为以后的财富。

## 对React和前端未来的展望

在这次专栏写作过程中，为了获得React 18新版本的一手资料，我阅读了大量React源码。老实说，这次阅读源码是比较辛苦的，一是写作节奏比较紧张，二是要纠正许多在React老版本中的概念和逻辑的理解，这里也要感谢专栏留言区部分同学们的输入。

当时也看到了React核心团队成员，对React的Fiber协调引擎和调度器的一些解释。当有网友问，这套异步机制是不是在为浏览器JS实现多线程？团队的回答很巧妙：“是，也不是。”

之所以回答“是”，是因为Fiber确实在使用一套自己的方式来分解和调度任务（工作），来避免浏览器线程被阻塞。之所以回答“不是”，是因为这套方式比多线程更加轻量，不涉及线程通信、线程同步/线程锁。

其实我也在想，保证工作不阻塞这件事本身，是不是应该交由浏览器来做？现代浏览器确实包含了类似技术，如Web Worker、WebAssembly甚至iFrame。但每个技术都有它原本的使用场景，如果拿来当成多线程来用，都会存在不少的Hack。

未来浏览器会不会为JS加入原生多线程？也许会，也许不会。单就目前的React技术而言，它已找到了适合它自己的技术路线，即Fiber。所以我理解React并不迫切需要浏览器原生支持多线程。

React以外的其他Web前端框架会引入Fiber吗？我认为机会不大，Fiber之所以适合React，不只是因为React面对的应用场景，更是因为React的历史包袱（说人家类组件是历史包袱有点过分吧？）。假设React推翻重来，从函数组件+Hooks开始重新设计开发，相信Fiber中的抽象层次一定会有所简化，调度逻辑也可能有相应的变化。

回到React API层面。一个框架的发展有点像企业扩张，企业的主要扩张方式包括**横向一体化**和**纵向一体化**，横向是指收编和自己类似其他的产业或产品，纵向是指把与自己相关的原材料、再加工这些产业链上下游收编进来。当然，如果企业不差钱，还可以完全不讲逻辑，东一榔头西一棒锤地搞投资。

React从0.14版一直到最新的18版，扩张是相当克制的。横向来看，在类组件体系基础上加入了函数组件+Hooks；纵向来看，收编了Redux的部分功能（useReducer）。其他就算加进来也无可厚非的功能，比如前端路由、表单验证、服务器通信，React框架一概不碰，完全交给React生态圈来补足。

React后面的版本会发生什么？你如果感兴趣可以多关注它的[官方博客](https://zh-hans.reactjs.org/blog/2022/06/15/react-labs-what-we-have-been-working-on-june-2022.html)。我个人也比较好奇，它会不会继续克制，或者在一定程度上转换关注点。

React之外的前端技术也在蓬勃发展。就像之前提到的，**历史的车轮会一直向前，但技术的轮子会时不时往回滚**。比如当网络延迟和服务器算力不再成为系统设计的瓶颈时，把重心放到服务器端的前端技术又卷土重来了（参考最近出圈的[htmx](https://htmx.org/essays/)技术）。

## 写在最后

给你分享两件我做专栏记忆最深刻的事。

1.对我来说，做专栏最难的部分，竟然是录音。我也说了几十年的话了，日常生活、工作中说话没有任何障碍，但朗读专栏的音频稿，就是会一而再再而三地出错。别的老师录一节课用40分钟，我却需要2个小时以上，录音笔的录音文件序号已近1800了。我建议你平时也可以试试录音这件事，还是挺锻炼人的。在这里，要感谢我夫人、老板和同事们的鼓励和支持。

2.我家养了两只猫，姐姐会坐在我键盘旁边看我打字，看我卡文时还会帮我敲几行进去（你看到的文稿中至少有100字是她敲的）；弟弟则会半夜踱步到书房门口，陪我熬夜写稿，但每次陪不到两分钟他自己就睡着了。

当然，最想感谢的还是陪我到结束语的你。你的学习、认真留言是我写作的最大动力。希望这个专栏能够助力你的React Web开发独当一面，帮助你在未来的工作中，把握住前端技术的变与不变，以成长，应万变。

我知道很多同学都喜欢“潜水”，但是在专栏的最后，我希望你能分享一下你的学习方法。此外，我给你准备了一份[毕业调查问卷](https://jinshuju.net/f/p2xO3M)，题目不多，希望你花两分钟填写一下，我会认真倾听你对这个专栏的意见或建议，期待你的反馈。

最后，再次感谢！不说再见，我们留言区见。

[![图片](https://static001.geekbang.org/resource/image/0c/b6/0c47a0c3e83cc13f14b72ba81bccddb6.jpg?wh=1142x801)](https://jinshuju.net/f/p2xO3M)
<div><strong>精选留言（9）</strong></div><ul>
<li><span>船长</span> 👍（4） 💬（1）<p>感谢宋老师的细腻又成体系的分享，完结撒花！

山高路远，江湖再见，他日相逢，再次杯酒言欢。</p>2022-11-03</li><br/><li><span>INFRA_UEX</span> 👍（3） 💬（1）<p>吾今三十有七，复有志于学矣。</p>2022-11-03</li><br/><li><span>莫比斯</span> 👍（0） 💬（1）<p>感谢宋老师的分享</p>2023-08-02</li><br/><li><span>潮汐</span> 👍（0） 💬（1）<p>学完打卡，后续继续加深React的学习。老师很耐心负责，点赞！</p>2023-01-04</li><br/><li><span>Eric</span> 👍（0） 💬（1）<p>感谢，讲的深入，清晰</p>2022-12-25</li><br/><li><span>Faith信</span> 👍（0） 💬（1）<p>打卡</p>2022-11-23</li><br/><li><span>Adu</span> 👍（1） 💬（0）<p>写到的真好，作为一个目前后端开始转全栈的，几年前在上家公司也用过react，当时就用的redux，中间这几年没做过react开发了，最近一年开始做全栈开发（公司需要），用了hooks，终于明白了hooks含义和redux的关系，真是tmd豁然开朗（请允许我爆了下粗口），感谢作者，写的真的是通俗易懂，循序渐进，用个看板例子串联了真个课程，我很少很少回复和发表看法（懒），今天打了这么多字，再次感谢下作者~  谢谢~</p>2024-04-03</li><br/><li><span>陈越</span> 👍（0） 💬（0）<p>老师是一个细致、幽默、有生活、有技术、有文笔的妙人，感谢一路陪伴，祝好！</p>2024-11-16</li><br/><li><span>lcl</span> 👍（0） 💬（0）<p>宋老师提到制作课程最难的部分是录音，深有同感，技术人很多是沉默寡言，能够说出来已经是很了不起了。又是没怎么说话的一天，以后我要多说说话，也可以尝试录音说点什么。不过，自己曾尝试用手机录音，感觉效果都不太好，有必要买只录音笔或话筒吗</p>2024-04-18</li><br/>
</ul>