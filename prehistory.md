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
 <p align="center"><sub><sup>(译者注：V神貌似把名字搞错了，对方叫Jeffrey不是Jeremy)</sup></sub></p>
 
 &nbsp;&nbsp;&nbsp;&nbsp;Gavin的最初贡献是两方面的。首先，你可能注意到了合约的调用模型最初的设计是异步的：虽然合约A可以给合约B创建一个“内部交易”（“内部交易”是Etherscan的术语，一开始它们只被叫做“交易”，后来叫“消息调用”或者“调用”），内部交易的执行只有在第一个交易的执行完全结束之后才会开始。这意味着交易不能用内部交易来获取其他合约的信息；唯一的方式是额外操作码（有点像SLOAD，你可以用它才读取其他合约的存储信息）。在Gavin和其他人的支持下，这个设计后来被摒弃。

&nbsp;&nbsp;&nbsp;&nbsp;在实现我最初的规范时候，Gavin自然的以同步方式实现了内部交易，他甚至没有意识到意图是不同的-也就是说，在Gavin的实现中，当一个合约调用其他合约，内部交易会被立刻执行，一旦执行结束，虚拟机会返回到创建该内部交易的合约并执行下一个操作码。我们两人都认为这个方案比最初设计更加优越，于是我们决定将其纳入规范。
其次，Gavin和我的某次讨论（发生某次旧金山散步中，所以具体细节已小事在历史的风中，也许会在美国国家安全局的深度档案会有一两份副本）导致了交易费模型的重构，从“合约付费”方式迁移到“发起方付费”方式，同时转向“燃料费”架构。与每个交易步骤立刻消耗以太币不同，交易的发起方支付并分配一些“燃料”（大约就是计算步骤的计数），计算步骤消耗这些燃料。如果交易耗尽的燃料，那么燃料仍旧丧失，但整个执行会被回退。这看起来是最安全的，它消除了之前合约必须担心的“部分执行”的安全隐患。当交易执行完成，未被消耗的燃料费将被退还。


&nbsp;&nbsp;&nbsp;&nbsp;Gavin在人们对以太坊的看法转变方面也功不可没。有些人把以太坊看作一个可编程的数字货币平台，基于区块链的合约，根据事先约定的规则持有和转移数字资产，他使人相信以太坊是一个通用目的的计算平台。这起源于一些关注点和术语的微妙变化，稍后随着“Web3”的概念深入人心而更具影响力。Web3把以太坊视为去中心化技术的一部分，去中心化技术的另外两个重要组成部分是whisper和Swam。

<img src="https://vitalik.ca/images/prehistory-files/web3suite.png" width="80%">

2014年初前后，以太坊也做了一些基于其他人建议的修改。在Andrew Miller和其他人的想法建议下，我们最终退回到基于栈的架构。

&nbsp;&nbsp;&nbsp;&nbsp;Charle Hoskinson 建议把从比特币的SHA256算法迁移到更新的SHA3（或者更确切的说是keccak256）。虽然一度有争议，但经过和Gavin，Andrew及其他人讨论之后，最终决定将栈的大小限制在32字节，另外一个考虑中替代的方案是无限制整数，它的问题在于很难对加法，乘法等其他操作计算应该收取多少燃料费。

![gavwoodmessage](https://vitalik.ca/images/prehistory-files/amiller2.png)

时间退回到2014年一月份，我们脑海中最初的挖矿算法是被称作Dagger的新玩意。

[https://github.com/ethereum/wiki/blob/master/Dagger.md](https://github.com/ethereum/wiki/blob/master/Dagger.md)

![dagger](https://vitalik.ca/images/prehistory-files/daggerspec.png)

&nbsp;&nbsp;&nbsp;&nbsp;Dagger的名称来源于其算法用了有向无环图（DAG）数据结构。其背后的思想是每隔N个区块，会从伪随机的种子产生一个新的DAG结构，DAG的底层是一组需要几个G空间来存储的节点。但是在DAG中产生每个值只需要计算几千个条目。一次“Dagger计算”需要从底层数据集的随机位置获取一些值，并将他们一起作哈希运算。这意味着有更快的方式去做Dagger计算-- 提前将DAG需要的数据缓存在内存。 同时，还有一种更慢但不耗内存的方式--每次都重新生成DAG需要的数据。

&nbsp;&nbsp;&nbsp;&nbsp;这个算法的目的是为了和当时流行的"memory-hardness"属性算法保持一致，比如Scrypt，同时还能对轻客户端友好。矿工们会采用更快的工作方式，所以他们的挖矿收到内存带宽的限制（理论上消费级别的内存已经重度优化了，所以很难在ASICS矿机上进一步优化），但是轻客户端可以用不好内存但是更慢的版本来进行验证。更快的方式可能需要几微秒，而幔的无内存的方式需要几毫秒，所以对轻客户端来说还是可行的。

&nbsp;&nbsp;&nbsp;&nbsp;从这开始，该算法在以太坊开发过程中改变了几次。我们经历的下一个想法是“自适应工作证明”；在这里，工作量证明将涉及执行随机选择的以太坊合约，并且有一个聪明的理由来解释这将具有“抗 ASIC 性”：如果ASIC被开发出来，其他竞争矿工将有动力创建和发布ASIC不擅长执行的合约。ASIC矿机没有通用性可言，因为它只是一个 CPU。所以我们可以利用这种对抗性激励机制来构建工作量证明，它本质上应执行通用计算。

&nbsp;&nbsp;&nbsp;&nbsp;这个计划失败的原因很简单 : 长程攻击。 攻击者可以从创世区块开始创建一条新链，只用简单的合约来填充它，这样他们可以为这些合约创建专门的硬件，迅速超过并取代主链。 所以 ... 我们只能推到重来。

&nbsp;&nbsp;&nbsp;&nbsp;我们考虑下一个算法叫随机电路，这个[Google文档]((https://docs.google.com/document/d/19c0L7_1neWpTN-jYwW-87mzrTTmS2h3lAYxXpRAvPfo))有详细描述。它是由我和Vlad Zamfir提出，并由Matthew Wampler-Doty和其他人审阅。这个想法是在挖矿算法中通过执行随机生成的电路来模拟通用计算。并没有确凿的证据表明它行不通，但是2014年间我们接触的硬件专家都对此表示悲观。Matthew Wampler-Doty本人建议基于SAT完备问题解决方案的算法，但这个提议最终被拒绝。

&nbsp;&nbsp;&nbsp;&nbsp;最后，我们又回到原点用一个叫做“Dagger Hashimoto”的算法。 有时简称为“Dashimoto”，它借鉴了 [Hashimoto](https://pdfs.semanticscholar.org/3b23/7cc60c1b9650e260318d33bec471b8202d5e.pdf) 的许多想法，这是 Thaddeus Dryja 提出的工作量证明算法，他开创了“I/O 密集工作量证明”的概念，其中挖矿速度的主要限制因素是不是每秒哈希数，而是每秒 RAM 访问数兆字节。但它同时结合了 Dagger算法中对轻客户端友好 DAG 生成数据集的概念。经过我自己、Matthew、Tim 和其他人的多次优化，这些想法最终融合到我们现在称为 [Ethash](https://github.com/ethereum/wiki/wiki/Ethash) 的算法中。

 ![Ultimate Scripting V2](https://vitalik.ca/images/prehistory-files/hashimoto.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;到2014年夏天的时候，以太坊协议已经相当稳定，一个重大例外是工作量证明算法要到2015年初才达到Ethash阶段，同时一份半正式的规范以Gavin的[黄皮书](http://gavwood.com/Paper.pdf)形式出现。
 
 ![Ultimate Scripting V2](https://vitalik.ca/images/prehistory-files/yellowpaper.png)
 
&nbsp;&nbsp;&nbsp;&nbsp;2014年八月，我开发引入了叔块机制，它允许以太坊区块链又更短的阻塞时间和更高的容量同时降低了中心化的风险。它是在POC6中被引进的。


&nbsp;&nbsp;&nbsp;&nbsp;和Bitshares团队的讨论，促使我们考虑把堆作为第一等数据结构，虽然最后我们因为缺乏时间而没能实现。而之后的安全审计和DoS攻击让我们明白，要安全的实现它，其难度比我们当时想象的更大。


&nbsp;&nbsp;&nbsp;&nbsp;9月，Gavin 和我计划了接下来对协议设计的两项重大更改。首先，除了状态树和交易树，每个区块还包含一个“收据树”。收据树将包括由交易创建的日志的哈希值，以及中间状态根。日志将允许交易创建保存在区块链中的“输出”，并且轻客户端可以访问这些输出，但未来状态计算无法访问。这可用于允许去中心化应用程序轻松查询事件，例如代币转移、购买、交易订单的创建和执行、拍卖的开始等等。
