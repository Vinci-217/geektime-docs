你好，我是徐昊。今天我们继续来进行代码评点。

上节课我们展示了在Higher-order function组合的函数风格下，进行TDD的节奏。我们还剩下最后一段类型函数没有做完：

接下来就是重构的环节：

重构虽然是修改代码的一种意图，但在21世纪的今天，我们讲重构的时候，特指在工具辅助下所做的自动化重构。因而随着使用的工具不同，我们所做的重构也应该有所不同。

可以说，无论使用什么样的语言，我们都应该找到那个对自动化支持最好的工具，这样才能让整个TDD的过程变得更加顺畅。这也是我在这次代码点评中，想特别提醒你注意的一点。

## 思考题

Higher-order function函数风格和对象风格在TDD的节奏上有什么不同？

**编辑来信**

> 如果你没有来得及参加此次代码评点活动，别担心，还有机会。我们在每个实战项目结束之际，都会开展“代码评点”活动。我们的要求依然是，跟上课程的更新节奏，多动手多实操多思考，最后填写学习反馈的问卷！  
> 　  
> 另外，可以加入我们的[读者交流群](https://jinshuju.net/f/zvOavT)，及时获取活动信息。也可以关注每节课的末尾部分，我会时不时地插播一些活动信息。

接下来我们将进入实战中的TDD环节，也就是使用TDD的方式，去实现我们工作中常用的技术框架。我们下节课再见！
<div><strong>精选留言（3）</strong></div><ul>
<li><span>Hacken</span> 👍（2） 💬（3）<p>老师好，如果可以，能否推荐一些开源项目在你看来应该是按照tdd的方式进行开发的？</p>2022-04-07</li><br/><li><span>keep_curiosity</span> 👍（2） 💬（0）<p>函数本身是无状态的。测试粒度可以很自然的按函数划分。如果依赖其他函数也很容易用测试替身代替（成本更低）。</p>2022-04-05</li><br/><li><span>zenk</span> 👍（0） 💬（0）<p>top-&gt;down vs bottom-&gt;up</p>2024-07-07</li><br/>
</ul>