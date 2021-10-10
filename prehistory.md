&nbsp;&nbsp;&nbsp;&nbsp;英文好的同学建议直接阅读Vitalik Buterin（V神）原文 [A Prehistory of the Ethereum Protocol
](https://vitalik.ca/general/2017/09/14/prehistory.html)
### 《以太坊协议史前回忆》



&nbsp;&nbsp;&nbsp;&nbsp;虽然当前以太坊协议背后的想法大体上已经成熟了两年多，但以太坊并未以目前的概念立刻面世并完全形成。在这条区块链启动之前，以太坊协议经历了数次重要的演变和设计决定。本文目的在于介绍以太坊协议诞生到启动经历的多次演变,而实现协议付出大量的工作, 比如 Geth， cppethereum， pyethereum, and EthereumJ，
以及以太坊生态上的应用程序和业务，则明显超出的本文范围。

&nbsp;&nbsp;&nbsp;&nbsp;Casper和分片研究也不在本文讨论范围。当然我们可以写更多的文章来讨论当年Vlad（*译者注：Vlad Zamfir
以太坊核心开发者*），Gavin(*译者注：Gavin Wood
以太坊黄皮书作者，前以太坊CTO*)，我还有其他人提出的各种想法，有些想法现已被抛弃，包括“工作量证明的证明”，hub-and-spoke链， "[Hypercubes](https://blog.ethereum.org/2014/10/21/scalability-part-2-hypercubes/)"，[影子链](https://blog.ethereum.org/2014/09/17/scalability-part-1-building-top/)（ 颇有争议的被认为是[Plasma](http://plasma.io/)的前身），Chain Fibers,Casper的多次迭代，还有Vlad在共识协议和属性中激励参与者的一些快速更新的想法，这些故事非常复杂，限于篇幅，无法详述，所以暂且跳过。


&nbsp;&nbsp;&nbsp;&nbsp;让我们先从最早期版本开始，它最终变成了以太坊，当时它甚至还不叫以太坊。2013年十月，当时我正在以色列访问，我花了很多时间和Mastercoin团队在一起，甚至为他们提供了不少功能建议。在多次思考他们在做什么之后，我给Mastercoin团队提交了一份提案，目的是将他们的协议通用化，支持更多合约类型，而不是增加同等规模的巨大复杂的功能：

[https://web.archive.org/web/20150627031414/http://vbuterin.com/ultimatescripting.html](https://web.archive.org/web/20150627031414/http://vbuterin.com/ultimatescripting.html)

 ![Ultimate Scripting](https://vitalik.ca/images/prehistory-files/ultimatescripting.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;注意这和后来愿景更为宏大的以太坊相去甚远：它只专用于Mastercoin团队已经在试图专用的地方，一个名为两方合约的功能，A方和B方都可以在合约中放入资金，稍后他们可以根据合约中的公式去获取资金（比如：赌约规定如果X事情发生，那么所有的资金归A方所有，否则所有资金归B方）。这个脚本语言是非图灵完备的。


&nbsp;&nbsp;&nbsp;&nbsp;虽然Mastercoin团队对这个提案感到惊艳，但他们没兴趣放弃目前正在做的事情来改变研究方向，而我日益相信这是一个正确的选择。下面是第二版，时间大约是12月份:

[https://web.archive.org/web/20131219030753/http://vitalik.ca/ethereum.html](https://web.archive.org/web/20131219030753/http://vitalik.ca/ethereum.html)

 ![Ultimate Scripting V2](https://vitalik.ca/images/prehistory-files/ethereumwhitepaper.png)