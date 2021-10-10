&nbsp;&nbsp;&nbsp;&nbsp;英文好的同学建议直接阅读Vitalik Buterin（V神）原文 [A Prehistory of the Ethereum Protocol
](https://vitalik.ca/general/2017/09/14/prehistory.html)


<h1 align="center"> 《以太坊协议史前回忆》 </h1>


&nbsp;&nbsp;&nbsp;&nbsp;虽然当前以太坊协议背后的想法大体上已经成熟了两年多，但以太坊并未以目前的概念立刻面世并完全形成。在这条区块链启动之前，以太坊协议经历了数次重要的演变和设计决定。本文目的在于介绍以太坊协议诞生到启动经历的多次演变,而实现协议付出大量的工作, 比如 Geth， cppethereum， pyethereum, and EthereumJ，
以及以太坊生态上的应用程序和业务，则明显超出的本文范围。

&nbsp;&nbsp;&nbsp;&nbsp;Casper和分片研究也不在本文讨论范围。当然我们可以写更多的文章来讨论当年Vlad（<sub><sup>*译者注：Vlad Zamfir
以太坊核心开发者*</sub></sup>），Gavin(<sub><sup>*译者注：Gavin Wood
以太坊黄皮书作者，前以太坊CTO*</sub></sup>)，我还有其他人提出的各种想法，有些想法现已被抛弃，包括“工作量证明的证明”，hub-and-spoke链， "[Hypercubes](https://blog.ethereum.org/2014/10/21/scalability-part-2-hypercubes/)"，[影子链](https://blog.ethereum.org/2014/09/17/scalability-part-1-building-top/)（ 颇有争议的被认为是[Plasma](http://plasma.io/)的前身），Chain Fibers,Casper的多次迭代，还有Vlad在共识协议和属性中激励参与者的一些快速更新的想法，这些故事非常复杂，限于篇幅，无法详述，所以暂且跳过。


&nbsp;&nbsp;&nbsp;&nbsp;让我们先从最早期版本开始，它最终变成了以太坊，当时它甚至还不叫以太坊。2013年十月，当时我正在以色列访问，我花了很多时间和Mastercoin团队在一起，甚至为他们提供了不少功能建议。在多次思考他们在做什么之后，我给Mastercoin团队提交了一份提案，目的是将他们的协议通用化，支持更多合约类型，而不是增加同等规模的巨大复杂的功能：

[https://web.archive.org/web/20150627031414/http://vbuterin.com/ultimatescripting.html](https://web.archive.org/web/20150627031414/http://vbuterin.com/ultimatescripting.html)

 ![Ultimate Scripting](https://vitalik.ca/images/prehistory-files/ultimatescripting.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;注意这和后来愿景更为宏大的以太坊相去甚远：它只专用于Mastercoin团队已经在试图专用的地方，一个名为两方合约的功能，A方和B方都可以在合约中放入资金，稍后他们可以根据合约中的公式去获取资金（比如：赌约规定如果X事情发生，那么所有的资金归A方所有，否则所有资金归B方）。这个脚本语言是非图灵完备的。


&nbsp;&nbsp;&nbsp;&nbsp;虽然Mastercoin团队对这个提案感到惊艳，但他们没兴趣放弃目前正在做的事情来改变研究方向，而我日益相信这是一个正确的选择。下面是第二版，时间大约是12月份:

[https://web.archive.org/web/20131219030753/http://vitalik.ca/ethereum.html](https://web.archive.org/web/20131219030753/http://vitalik.ca/ethereum.html)

 ![Ultimate Scripting V2](https://vitalik.ca/images/prehistory-files/ethereumwhitepaper.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;你可以看到大量重新架构的结果，这主要是由于我在11月份在旧金山进行了一次长途步行，期间我意识到智能合约可以完全通用化。与用脚本语言简单描述双方关系条款不同，合约本身是更加完善的账户，能够持有，发送，收取资产，并且还可以维护持久存储（当时，持久存储被称为“内存”，而唯一的零时“内存”是256个寄存器）。把脚本语言从基于栈的机器切换到基于寄存器，是我自己的决心。除了看起来更加复杂外，其他方面我毫无异议。

&nbsp;&nbsp;&nbsp;&nbsp;此外，请注意收费机制内置其中：

![transcation fee](https://vitalik.ca/images/prehistory-files/txfee.png)


&nbsp;&nbsp;&nbsp;&nbsp;从这点上来讲，以太币就是燃料费；单个计算步骤之后，交易调用的合约对应的余额会减少一些，如果合约余额耗尽，执行会停止。注意这种“接收者付费”的机制意味着合约本身必须要去发送者支付一笔费用，如果费用不存在则立即退出；以太坊协议预先分配了16个执行步骤的费用，以便合约来拒绝未付费的交易。

&nbsp;&nbsp;&nbsp;&nbsp;当时以太坊协议还知识我一个人的创意。但从那时起，新的参与者开始加入团队，Gavin Wood在协议层的贡献是最为显著的。2013年十二月，他通过about.me网站发消息联系到我：

 ![gavwoodmessage](https://vitalik.ca/images/prehistory-files/gavwoodmessage.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;Jeffrey Wilcke, Go客户端的主程序员 (当时项目名称叫“ethereal”)也在同一时间联系我并贡献代码， 不过他的贡献更多是在客户端开发方面而非协议研究。
 
 ![gavwoodmessage](https://vitalik.ca/images/prehistory-files/jeffreywilcke.png)
 <p align="center"> "你好Jeremy, 很高兴看到你对以太坊有兴趣..." </p>
 <p align="center"><sub><sup>*(译者注：V神貌似把名字搞错了，对方叫Jeffrey不是Jeremy)*</sup></sub></p>
 
 &nbsp;&nbsp;&nbsp;&nbsp;Gavin的最初贡献是两方面的。首先，你可能注意到了合约的调用模型最初的设计是异步的：虽然合约A可以给合约B创建一个“内部交易”（“内部交易”是Etherscan的术语，一开始它们只被叫做“交易”，后来叫“消息调用”或者“调用”），内部交易的执行只有在第一个交易的执行完全结束之后才会开始。这意味着交易不能用内部交易来获取其他合约的信息；唯一的方式是额外操作码（有点像SLOAD，你可以用它才读取其他合约的存储信息）。在Gavin和其他人的支持下，这个设计后来被摒弃。

&nbsp;&nbsp;&nbsp;&nbsp;在实现我最初的规范时候，Gavin自然的以同步方式实现了内部交易，他甚至没有意识到意图是不同的-也就是说，在Gavin的实现中，当一个合约调用其他合约，内部交易会被立刻执行，一旦执行结束，虚拟机会返回到创建该内部交易的合约并执行下一个操作码。我们两人都认为这个方案比最初设计更加优越，于是我们决定将其纳入规范。
其次，Gavin和我的某次讨论（发生某次旧金山散步中，所以具体细节已小事在历史的风中，也许会在美国国家安全局的深度档案会有一两份副本）导致了交易费模型的重构，从“合约付费”方式迁移到“发起方付费”方式，同时转向“燃料费”架构。与每个交易步骤立刻消耗以太币不同，交易的发起方支付并分配一些“燃料”（大约就是计算步骤的计数），计算步骤消耗这些燃料。如果交易耗尽的燃料，那么燃料仍旧丧失，但整个执行会被回退。这看起来是最安全的，它消除了之前合约必须担心的“部分执行”的安全隐患。当交易执行完成，未被消耗的燃料费将被退还。


&nbsp;&nbsp;&nbsp;&nbsp;Gavin在人们对以太坊的看法转变方面也功不可没。有些人把以太坊看作一个可编程的数字货币平台，基于区块链的合约，根据事先约定的规则持有和转移数字资产，他使人相信以太坊是一个通用目的的计算平台。这起源于一些关注点和术语的微妙变化，稍后随着“Web3”的概念深入人心而更具影响力。Web3把以太坊视为去中心化技术的一部分，去中心化技术的另外两个重要组成部分是whisper和Swam。

 ![gavwoodmessage](https://vitalik.ca/images/prehistory-files/web3suite.png)
