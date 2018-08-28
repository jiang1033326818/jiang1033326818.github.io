---
layout:     post
title:      关于Hyperledger   Fabric的一些问题和总结
subtitle:   区块链  能源互联网
date:       2018-08-30
author:     BY
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - 区块链
    - 开发技巧
	- Hyperledger
	- Fabric
---

已经有半年没有更新博客了,主要是最近遇到了一些问题,心情很差,不过近期已经调整过来了,继续更新

最近区块链火的一塌糊涂,于是我在Oracle的社区总结了一些关于区块链3.0的代表Hyperledger的一些问题


* 联系方式
	* [我的QQ](http://wpa.qq.com/msgrd?v=1&uin=1033326818&site=qq&menu=yes)
    * [我的微博](https://weibo.com/u/5209344262)
	* [我的知乎](https://www.zhihu.com/people/jiang-hai-peng-93/activities)
	* [我的github](https://github.com/jiang1033326818)
	
	

## Hyperledger是什么？

Hyperledger （超级账本）是一个开源的区块链和相关工具的总括项目，由 Linux基金会在2015年12月发起该项目，以支持基于区块链技术的去中心化账本的协作开发。详细信息可参考如下官方网站: https://www.hyperledger.org/

##  Hyperledger框架项目主要包含哪些？

Hyperledger项目孵化了众多开源项目，总体分为框架和工具两大类，其框架项目主要有以下几个：

a) Hyperledger Sawtooth

b) Hyperledger Iroha

c) Hyperledger Burrow

d) Hyperledger Indy

e) Hyperledger Fabric

以上框架类项目中，每个项目都有各自的设计理念和特色，支持的共识算法、开发语言各不相同。目前只有Sawtooth和Fabric达到了生产稳定状态，可以应用于企业开发。而Fabric是目前最流行、使用最广泛的企业级框架。

工具类项目，目前有：Blockchain-explorer、Cello、Composer等。
## Hyperledger Sawtooth是什么？

Hyperledger Sawtooth是Intel贡献和主导的分布式账本技术平台，它支持PoET（Proof of Elapsed Time）和Quorum Voting两种共识机制，当节点数量很多（公有链环境）时，使用第6代Intel Core CPU所提供的SGX扩展功能提供的一种称为时间流逝证明PoET的机制来形成共识，它的性能和可靠性由Intel CPU硬件来保障，PoET算法以最少的资源消耗为目标，使我们能以较少的能源消耗建立数百至数千个节点的非常广泛和扁平的区块链网络，是公有链系统里很有价值的一个共识机制。

另一方面，当节点数量少且受控时，Sawtooth可以采用法定人数投票Quorum Voting共识机制，Quorum Voting是瑞波币和恒星币的修正版，用于满足需要即时确定交易的应用场景，非常适合于联盟链场景，这样Sawtooth就摇身一变成为很好用的联盟链了。

所以Sawtooth既可以用于需要许可的联盟链中，也可以用于不需要许可的公有链中。另外，Sawtooth提供的SDK比较多，有Go, C++, Java, Node.js, Python等。
## Hyperledger Burrow是什么？

Hyperledger Burrow是由 Monax贡献，Intel共同赞助的智能合约解释器。它是超级账本Hyperledger中第一个来源以太坊的项目，是第一个采用以太坊虚拟机（EVM）标准的带权限许可的智能合约解释器。Burrow对EVM做了一些扩展，同时保持与EVM兼容。Burrow被设计成一个通用的智能合同机器，采用对PBFT做了优化的Tendermint共识算法，有比较好的性能。

借助遵循Apache许可的以太坊虚拟机Burrow，使Hyperledger中的其他分布式账本项目（比如Fabric、Sawtooth、Lake、Iroha）可以将EVM融合到各自的平台，比如通过与Burrow集成，Sawtooth已经可以支持以太坊的智能合约。这也意味着超级账本组织和以太坊社区，包括企业级以太坊联盟，开始建立一种富有成效的关系。

## Hyperledger Iroha 是什么？

Hyperledger Iroha是由日本公司Soramitsu发起和贡献的轻量级分布式账本，它的设计和架构参考Fabric。Iroha的目标是：

a) 为C++开发人员提供一个为Hyperledger做出贡献的环境，在C++中创建可重用组件来补充Fabric、Sawtooth和其他潜在项目，这些组件可以使用Go等语言进行调用；

b) 为移动和Web应用程序支持提供基础设施（提供iOS, Android和JavaScript类库）；

c) 提供一个框架来试验新的API和共识算法，这些算法可能会在将来被纳入Fabric。

此外，Iroha还支持数字资产(Digital Asset)的发行。

## Hyperledger Indy是什么？

Hyperledger Indy由Sovrin基金会贡献，Sovrin基金会成立于2016年，致力于打造一个基于区块链的去中心化的全球数字身份自治管理的公共基础设施。Indy提供了工具、程序库和可重复使用的组件，用于提供基于区块链或者其它分布式账本的数字身份，从而让它们可以跨账本、跨管理域、跨应用进行互操作。Indy为Fabric、SawtoothLake、Corda等提供了强大的跨账本身份管理功能。

由于分布式账本事后无法更改的特点，因此基于分布式账本的身份用例应仔细考虑基本组件，包括性能，规模，信任模型和隐私保护。Hyperledger Indy开发了去中心化身份的规范，术语和设计模式，并实现了这些概念，可以在Hyperledger联盟内部和外部使用。

## Hyperledger Fabric是什么？

Hyperledger Fabric是来源于IBM的分布式账本技术平台，是目前为止在设计上最贴近联盟链思想的区块链，Fabric有完备的权限控制和安全保障，数据保密机制，它采用模块化设计，可插拔架构，允许组件（如共识算法和会员管理）即插即用。 Hyperledger Fabric利用容器技术来运行称为Chaincode的智能合约。Fabric获得众多重量级企业的支持，是目前应用最广泛的企业级区块链框架。

## Fabric的技术特点是什么？

同其他的主流的开源区块链技术平台相比，Fabric有以下特点：

a) Fabric有完备的权限控制和安全保障，兼顾数据共享和隐私保护。

b) Fabric采用模块化设计，可插拔架构，Key-Value数据库，身份管理，共识机制和加密算法等都是可插拔的，可以根据实际情况选择替换。

c) 同其他几种主流的开源技术框架相比，Fabric有更高性能和更好的扩展性。

d) Fabric提供多种语言的SDK，可根据实际的项目需要选用。

## Fabric的成员管理(Identity)主要有什么功能？

Identity，也就是成员管理，Fabric是目前为止在设计上最贴近联盟链思想的区块链。联盟链考虑到商业应用对安全、隐私、监管、审计、性能的需求，提高准入门槛，成员必须被许可才能加入网络。Fabric成员管理服务为整个区块链网络提供身份管理、隐私、保密和可审计的服务。

## Fabric的Transactions是什么？

Fabric上的Transactions事务分两种，部署事务(Deploy Transactions)和调用事务(Invoke Transactions)。

a) 部署事务把链码(Chaincode)部署到Peer节点上并准备好被调用，当一个部署交易成功执行时，Chaincode就被部署到各个Peer节点上，类似于把一个Web应用部署到应用服务器上的不同实例上。

b) 调用事务在先前部署的链码的上下文中执行操作。客户端应用程序通过Fabric提供的API调用先前已部署好的某个Chaincode的某个函数执行事务，包括读取和写入状态数据库，返回结果等。

## Fabric的智能合约Smart Contract是什么？

Fabric的智能合约Smart Contract称为链码Chaincode，是一段代码，它处理网络成员所同意的业务逻辑。和以太坊相比，Fabric链码和底层账本是分开的，升级链码时并不需要迁移账本数据到新链码当中，真正实现了逻辑与数据的分离。

## Fabric的账本(Ledger)数据是如何共享的？

Fabric的账本共享方式和比特币等有所不同。诸如比特币和以太坊，交易数据大家都可以查看，虽然不知道是谁的数据，但是数据本身是对所有人都可见共享的。但在 Fabric中，账本不是共享给所有人的。而是通过 Channel 隔离数据，虽然大家都在同一个区块链网络里，但是不在同一个Channel，也没办法共享账本。所以，通过建立不同的Channel可以达到按需共享的目的。

## Fabric的业务网络由什么组成？

业务网络，也叫共识网络或区块链网络，Fabric业务网络由不同的节点构成。节点是区块链的通信实体，节点是一个逻辑概念，不同类型的节点可以运行在同一台物理服务器上。这些节点可能部署在云上面或者本地。可能来自不同的公司或者组织。在区块链网络中有两种类型的节点：Peer节点和Orderer节点。

##  Fabric里的Peer节点有哪些？

Peer节点目前有两种： 背书节点Endorser和提交节点Committer。

a) Endorser 完成对交易提案的背书处理。主要工作是验证签名，进行权限和合法性检查，检查通过则模拟运行交易，对交易导致的状态变化（读写集）进行背书并返回结果给客户端。

b) Committer 负责维护区块链和账本结构。对从Orderer发送来的批量交易区块数据结构，进行最终检查（包括交易消息结构、签名完整性、是否重复、读写集合版本是否匹配等），检查通过后执行合法的交易，将结果写入账本。

## Fabric里的Orderer节点的作用是什么？

Orderer节点主要用于对事务进行排序（共识），批量打包，生成区块，发给Peer节点。一个区块链网络中会有多个Orderer节点，它们共同提供排序服务。排序服务可以实现为多种不同的方式，从一个中心化的服务（被用于开发和测试，如Solo），到分布式协议（如Kafka），再到PBFT的共识方式等。

## 如何基于Fabric开发区块链智能合约？

Fabric的智能合约Smart Contract称为链码Chaincode，是一段代码，它处理网络成员所同意的业务逻辑。目前支持用Go、Java、Node.js语言进行开发。

## 如何基于Fabric开发客户端的应用？

Fabric目前提供的SDK支持：Go、Python、Node.js和Java。前端应用通过SDK调用服务端的智能合约Chaincode。有些BaaS(Blockchain as a Service)云平台也提供REST接口，方便客户端调用后端的智能合约。

## Fabric上开发好的应用如何部署？

Fabric上开发好的前端应用的部署和传统应用没什么不同，可部署在应用服务器或者云服务上。后端开发的主要工作是写智能合约，实现业务逻辑，可以部署在区块链云服务上或者自己搭建的本地Fabric环境上。

Fabric目前最新的版本是多少？

截止到2018年3月，最新发布的是1.1版本。1.1相比1.0版本多了以下一些功能：

a) 可以采用Node.js开发Chaincode。

b) 基于通道的事件服务 - 使客户能够按每个通道订阅区块和区块事务（交易）事件。

c) 可以把CouchDB索引和Chaincode一起打包，以提高性能。

d) 能够动态更新客户身份和隶属关系。

e) Node.js SDK连接配置文件可简化与Fabric节点的连接。

f) 性能提升，提高了交易吞吐量，并降低了响应时间。

## Fabric在安全方面有哪些优势？

企业比较重视安全性， Fabric有以下一些优势：

a) 成员必须被许可才能加入网络，通过证书、加密、签名等手段保证安全。

b) 通过多通道Channel功能实现数据访问控制和隔离，保证只有参与交易的节点能访问到数据，其他的节点看不到。满足数据保护方面的法律法规要求。如有些行业，需要知道谁访问了特定的数据。

c) 另外Fabric的加密算法也是可插拔的，可替换的。

## 企业如何快速上链？

企业快速上链可以采用两种方式：一是基于Hyperledger自行搭建，但周期较长；二是选择在BaaS(Blockchain as a Service)云平台上构建自己的应用，享受云计算的快速部署、按需付费、弹性扩展等好处。

## Fabric为什么成为企业区块链框架的首选方案？

Fabric具有一些重要特性满足企业的需求，企业选择区块链技术框架主要考虑的因素有：框架的身份管理、框架的可扩展性、框架的企业安全性、框架的性能、业务逻辑实现、开放的API以及是否提供主流语言的SDK等。

