# 使用转移网关在以太坊和PlasmaChain之间转移ERC721代币

> 这是从其他网站上摘下来的 loom 公司使用的跨链技术

在我们之前的文章中，我们讨论了如何开始设置开发环境并将第一个DApp部署到Loom PlasmaChain测试网络。 

PlasmaChain是一个DPoS链，这意味着与以太坊主网络不同，参与块创建的节点数量仅限于几台功能强大的机器。虽然这对事务吞吐量和计算时间非常有利，但这也意味着PlasmaChain（以及任何其他以太坊侧链）的安全性将低于以太坊主网络。 

传输网关通过其在PlasmaChain上创建的大量节点网络和数字资产验证者，提供了由以太坊网络保证的相同级别的安全性。顾名思义，它们共同形成一组网关，您可以通过它们将ERC721（以及即将发布的ERC20）资产转移到以太坊主网络和其他智能合约链。 

传输网关分为四个部分：

1.以太坊网关
2. PlasmaChain网关
3. PlasmaChain地址映射器
4. Gateway Oracle

使用转移网关在以太坊和PlasmaChain之间转移ERC721代币

让我们逐一理解这个原则。 

以太坊和PlasmaChain网关
当有存款事件时，以太网网关和网关Oracle进行通信。这是与网关Oracle通信的机制。 PlasmaChain Gateway与以太网网关大致相同，只不过它是PlasmaChain的终点。 

PlasmaChain地址映射器
PlasmaChain地址映射器的存在是为了在多个链上实现“多个帐户”的概念。通过在地址映射器上注册帐户，您可以接收ERC721令牌，因为它们已存储在PlasmaChain中。 

网关Oracle 
Gateway Oracle负责在以太坊（在其他链中）和PlasmaChain之间进行通信。它通常在充当PlasmaChain验证者的节点上运行，但它也可以独立运行。它监控来自以太坊或PlasmaChain的网关活动，以监控存款和取款事件。当它收到一个事件时，它会向另一个链发出一个事务。


样品交易

现在让我们详细介绍一下。 

老王刚刚在以太坊主网站上使用了水系统来更换消防办公卡。他希望将新收购的消防局转移到PlasmaChain用于“Zombie Battlefield”，这是一款建立在PlasmaChain上的游戏。 

法老必须在PlasmaChain地址映射器中注册他的以太坊帐户。只需注册一次。 

为了证明法老拥有以太坊帐户，法老将向PlasmaChain地址映射器创建一个请求，以提供由他的以太坊帐户公钥签名的邮件。 PlasmaChain地址映射器将以太坊公钥映射到发出映射请求的PlasmaChain帐户。 

法老现在准备在两条连锁店之间移动代币。 

第一步是将令牌存入以太坊网关。这会将令牌的所有权转移到网关并发出存款事件。 

第二步是Gateway Oracle收到此存款事件，因为它订阅了以太坊和PlasmaChain网关事件。然后，Gateway Oracle执行以下两种操作之一：

如果PlasmaChain上不存在令牌，它将根据这些规范“转换”新令牌，其所有者将是PlasmaChain网关。然后它将可用于存款人的PlasmaChain账户，并作为存款交易的一部分。 

如果PlasmaChain Gateway已经拥有此令牌（如果它最初是在PlasmaChain上创建的，然后移动到另一个链，这可能会发生），那么可以从存款人的PlasmaChain帐户中检索它。 

最后，通过他的PlasmaChain帐户，Pharaoh可以通过PlasmaChain网关发送提款请求，然后接收令牌。 

如果法老想要在以太坊与其他人交换这张新卡，或者如果他想在他的以太坊钱包中存放稀有卡而不是用于安全的PlasmaChain钱包，他将来自PlasmaChain。网关发送传输请求，该请求由网关Oracle接收并签名。然后他可以拿出提款收据到以太坊。 

如何将ERC721令牌连接到传输网关

如果您是DApp开发人员并且想要发布可转移的ERC721令牌，您可能想知道如何将ERC721令牌连接到传输网关。 

第一步是在PlasmaChain和Ethereum上部署ERC721合同。合同不需要特殊，因为存款功能只是将令牌的所有权从用户转移到网关合同。但是，最好包括depositToGateway或类似功能，这些功能可以专门转移到已知的网关合同地址，这样您的用户就不必每次都填写网关地址。 
Pragma solidity ^ 0.4.24;  
导入'openzeppelin-   solidity/contracts/token/ERC721/ERC721Token.sol'; 
合同MyAwesomeToken是ERC721Token（'MyAwesomeToken'，'MAT'）{   //主网网关地址  地址公共网关; 
构造函数（地址_gateway）public {   gateway=_gateway; 
} 
函数depositToGateway（uint tokenId）public {      
  safeTransferFrom（msg.sender，gateway，tokenId）;  }  
} 
在两个链上部署ERC721令牌合约后，您需要在它们之间创建映射。这会将您的令牌“注册”到网关。在此示例中，我们将在Einfair测试网络（Rinkeby）和PlasmaChain测试网络（extdev）之间创建映射。 

在撰写本文时，Rinkeby传输网关的地址是：0x6f7Eb868b2236638c563af71612c9701AC30A388 

由于这是一个测试网络，因此网关合同可以由织机团队清除并重新部署。因此，请务必检查SDK文档端的当前地址。 

通过使用两个ERC721令牌合同的地址并证明您具有这些合同的签名，您可以通过调用extdev网关合同的addContractMapping函数来完成映射。 

要证明您已将ERC721合同部署到其中一个以太坊网络，您必须提供签名（在使用部署合同的以太坊私钥签名消息时生成签名）和部署合同的以太坊事务散列。 

更容易证明您已将ERC721合同部署到PlasmaChain。您只需要签署发送到PlasmaChain网关的请求，并使用部署合同的密钥来注册您的合同。然后，PlasmaChain Gateway将确保您的密钥是已部署合同的所有者。 

样品申请

为了更简单的解释，我们有一个很好的示例应用程序，您可以看到如何设置部署并使用loom-js来完成这些任务。 Loom-js是一个javascript库，可以帮助您处理签名事务和与传输网关交互等事情。整个类（“传输网关”）用于提供一种简单的方法来执行诸如在链之间映射ERC721协议之类的事情。 

可以在Loom SDK文档中找到Transfer Gateway示例应用程序和loom-js。 

转移到网关示例时，最有用和最有价值的文件之一是gateway-cli.js，因为它提供了一个很好的部署工具，您可以根据自己的合同进行修改或直接使用它。在撰写本文时，链接Rinkeby和extdev的地址被硬编码到gateway-cli.js中，因此如果它们与文档中列出的不同，则可能需要更新它们。