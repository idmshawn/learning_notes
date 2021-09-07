
# DDD读书笔记
DDD中，三个基本用途决定了模型的选择：
1. 模型和设计的核心相互影响；
2. 模型是团队所有成员所使用的交流语言的中枢；
3. 模型是浓缩的知识；

书中Ch1~4浏览即可，Ch5/6/14为DDD实现方法，需精读或复读。

## Ch1：消化知识
### 1.1 有效建模的要素
通过作者与PCB工程师共同建模的故事，提炼出建模案例成功的要素：
- 模型和实现绑定(一致)；
- 统一到基于模型的语言；(团队成员、开发人员和领域业务专家使用一种公共的建模语言)
- 开发一个蕴含丰富知识的模型；
- 提炼模型；(去粗取精，类似前言的中国地图)
- 头脑风暴和实验；(校对模型)

### 1.2 知识消化
知识消化，一般是在开发人员的领导下，由开发人员与领域专家组成的团队来共同协作。

强调了不能按照业务专家-->分析师-->程序员的单向、单次反馈，与WB课程所提一致；

### 1.3 持续学习
### 1.4 知识丰富的设计
通过航船超额订货单示例讲述了好的模型设计有助于突出重点项，能让业务专家和程序员都能明显找到超额订货策略。
### 1.5 深层模型
随着对领域和应用需求的理解逐步加深，模型中原本表面看起来重要的元素可能会被移除；开始时不被发现的抽象可能会成为问题要害。

要想建立实用且清晰的模型，团队成员需持续学习，既要精通领域业务知识，也要精通建模技术。

## Ch2：语言的交流和使用
### 2.1 模式：Ubiquitous language(通用语言)
语言不统一会造成相互理解错误、概念混淆等；引入翻译使得沟通不畅，导致知识消化变得困难；

领域模型可以成为公共语言的核心；Ubiquitous language的词汇表包含**类名称**和**主要操作**;

“知识消化过程”依赖“基于模型的语言的使用”。

![ubiquitous_lang](p40)

通过相似的两段对货运建模的示例说明通用语言在交流中所起的积极作用。

### 2.2 “大声地”建模
![exampl，对比的示例](p43)
讨论系统时要结合模型。使用模型的元素以及模型中各元素之间的交互来大声描述场景，并且按照模型允许的方式将各种概念结合到一起。找到更简单的表达方式来讲出你要讲的话，然后将这些新的思想应用到图和代码中。

### 2.3 一个团队，一种语言
![jiaoji](图2-3)

### 2.4 文档和图
作者画图以UML中的类图和对象交互图(或序列图)为主；但UML图无法传达模型的两个最重要的方面：一是模型所表示的概念的意义，另一方面是对象应该做哪些事情。

应避免使用包罗万象的对象模型图，甚至不能使用包含所有细节的UML数据存储库。应使用简化的图，图中只包含对象模型的重要概念部分，这些部分对于理解设计至关重要。

设计的重要细节应该在代码中体现出来。通常的用法是以图为主，辅以文本注释。作者更愿意以文本为主，添加精心挑战的简化图作为注释。

务必要记住*模型不是图*。图的目的是帮助表达和解释模型。代码可以充当设计细节的存储库。

#### 2.4.1 书面设计文档
- 文档应作为代码和口头交流的补充。
> - 极限编程不主张使用过多的设计文档，而是让代码解释它自己(因为注释和文档都可能出现于实际运行代码的不同步)。但作者指出，完全将代码作为一种设计文档也存在的局限性：会把读代码的人淹没在细节中；且开发人员并不是唯一需要理解模型的人。
> - 文档不应再重复表示代码已经明确表达出的内容。文档应将注意力集中在核心元素上，当代码无法直接明了地实现概念时，文档可以澄清设计意图。

- 文档应努力寻求生存之道并保持最新
> - 文档必须深入到各种项目活动中去。 判断方法：观察文档与Ubiquitous language之间的交互。
> - 通过将文档减至最少，并且主要用它来补充代码和口头交流，就可以避免文档与项目脱节。

#### 2.4.2 完全依赖可执行代码的情况
XP社区几乎完全依赖可执行代码和代码测试。但依赖开发人员的自律。

### 2.5 解释性模型
核心思想是在实现、设计和团队交流中使用同一个模型作为基础。但为了学习领域，还可以引入其它视图，这些视图仅用作传递一般领域知识的教学工具。

解释性模型可用于澄清范围伤受到严格限制的技术模型。**解释性模型最好不是对象模型，可避免人们错误地认为这些模型与软件设计是一致的**。

![示例](图2-4及图2-5)

## Ch3：绑定模型和实现
领域驱动设计要求模型不仅能够指导早期的分析工作，还应该成为设计的基础。

### 3.1 模式：Model-Driven Design
严格按照基础模型来编写代码，能够使代码更好地表达设计含义，并且使模型更符合设计。

Model-Driven Design不再将分析模型(目的是对领域进行抽象)和程序设计(目的是解决应用程序的问题)分离开，而是寻求一种能够满足这两方面需求的单一模型。MDD绑定了模型和程序设计。
- 如果模型对于程序的实现来说显得不太实用时，必须重新设计它；
- 如果模型无法忠实地描述领域的关键概念，也必须重新设计它；
这样，建模和程序设计就结合为一个统一的迭代开发过程。

### 3.2 建模范式和工具支持
过程语言(C语言)没有适用的建模范式，并不适用于Model-Driven Design。

**面向对象设计**是目前大多数大型项目所使用的建模范式，也是本书使用的主要方法。

PCB布线中net元素的示例：
- 用类图完成了一个简化的领域建模；
- 依照模型写出了java代码，Abstract Net父类，和Net子类，及其方法；
- Serveice和Repository都可以进行单元测试，给出了基于JUnit的测试框架；

据上例得出Model-Driven Design的好处：
- 易于拓展：能够为规则的组合设置限制条件，还能提供其他的一些增强功能；
- 方便测试：组件都具有定义完善的接口，可进行单元测试。

设计不是一蹴而就的，需要反复研究领域知识，不断重构模型，才能将领域中重要的概念提炼成简单而清晰的模型。

### 3.3 揭示主旨：为什么模型对用户至关重要
通过IE浏览器收藏夹不支持非法字符的例子，说明模型对用户的作用。

### 3.4 模式：Hands-on Modeler
将分析、建模、设计和编程工作完全分离会对Model-Driven Design产生不良影响。

作者参与项目的反面例子，建模人员不被允许参与代码实现，两部分完全脱钩；
模型没有派上用场，原因：
1. 将模型传递给开发人员的过程中，模型中的一些意图并没有向他们说明；
2. 模型与程序实现及技术相互影响，而我无法直接获得这种反馈。

Model-Driven Design的两个基本要素：**模型要支持有效的实现**并**抽象出关键的领域知识**；
总结：P62中间黑体字。

## Ch4：分离领域
![model-driven-design语言的导航图](p64)
### 4.1 模式：Layered Architecture
面向对象程序中广泛采用Layered Architecture模式。
Layered Architecture的基本原则是层中的任何元素都仅依赖于本层的其它元素或其下层的元素。向上的通信必须通过间接的传递机制进行。
多数分层机制按以下四层划分
- 用户界面层(或表示层)
- 应用层：尽量简单，不包含业务规则或者知识，只为下一层中的领域对象协调任务，分配工作，使它们相互协作。
- 领域层(或模型层)，领域层是业务软件的核心；“负责处理基本业务规则的是领域层，而不是应用层”；
- 基础设施层

总结：“领域对象应该讲重点放在如何表达领域模型上，。。。”
![分层](p67黑体)

示例：网上银行功能分层。

#### 4.1.1 将各层关联起来
最早将用户界面层与应用层和领域层相连的模式是Model-View-Controller(MVC)框架。

只要连接方式能够维持领域层的独立性，保证在设计领域对象时不需要同时考虑可能与其交互的用户界面，那么这些连接方式就都是可用的。

#### 4.1.2 架构框架
基础设施层作为service实现、MVC及类似的框架实现--》架构框架

应明确使用“架构框架”的目的：建立一种可以表达领域模型的实现，并且用它来解决重要问题。
不妄求完全之策，而是有选择性地运用框架来解决难点问题(选择框架中最具价值的功能能够减少程序实现和框架之间的耦合)，就可以避开框架的很多不足之处。

### 4.2 模型属于领域层
领域驱动设计只需要一个特定的层存在即可。

将领域实现独立出来是领域驱动设计的前提。

### 4.3 模式：The Smart UI “Anti-Pattern” (可略过)
smart UI，另一种设计方法，与DDD迥然不同且互不兼容。

DDD应用在大型项目上才能产生最大的收益。有学习成本。SmartUI则将无分层架构，但门槛低，适用开发人员经验较少的小型项目。

### 4.4 其它分离方式(可略过)

## Ch5：软件中所表示的模型
着重区分用于表示模型元素的三种模式：Entity、Value Object和Service。

### 5.1 关联
对象之间的关联使得建模与实现之间的交互更为复杂，**建模需强化突出重要的关联，弱化不必要的关联**。
三种使得关联更易于控制的方法：
- 规定一个遍历方向；
- 添加一个限定符，以便有效地减少多重关联；
- 消除不必要的关联；

简化和约束模型的关联是通往Model-Driven Design的必经之路。

### 5.2 模式：Entity(又称为 Reference Object)
很多对象不是通过它们的属性定义的，而是通过一连串的连续事件和**标识(Id)**定义的。

***主要由标识定义的对象被称作Entity***。它的生命周期中，形式和内容可能发生改变，但标识保持不变。事物作为Entity的两个条件：
1. 它在整个生命周期中具有连续性；
2. 它的一些对用户来说非常重要的不同状态不是由属性决定的。 ？？？

#### 5.2.1 Entity建模
- 不要将注意力集中在属性或行为上，应摆脱细节，抓住Entity对象定义的最基本特征：用于识别、查找或匹配对象的特征。
- 只添加对概念至关重要的行为及行为必须的属性。
- 应将行为和属性转移到与核心实体关联的其它对象中。

#### 5.2.1 设计标识操作
唯一标识的获取
- 通过具有唯一性的数据属性或属性组合，或属性加上简单约束使其具有唯一性；
- 没有真正唯一的key时，为每个实例附加一个类中唯一的符号。

系统中存在同一个对象的多个版本时(如在多个计算机系统之间确保唯一性)，问题解决方案：
第三方机构发放标识。或其它领域内方案。

### 5.3 模式：Value Object
很多对象没有概念上的标识，它们描述了一个事物的某种特征。

***用于描述领域的某个方面而本身没有概念标识的对象称为Value Object。***

@ Entity需要系统跟踪并处理其标识(或管理标识)，Value Obj则不需要。

- Value obj例子：颜色、字符串和数字。同一个事物在不同模型下，可能是entity，也可能是value obj，见地址的例子。
- Value obj经常作为参数在对象之间传递消息；常常是临时对象，创建后会被销毁。
- Value obj可以作为entity或其它value的属性；Value obj也可以引用entity。

当我们只关心一个模型元素的属性时，应把它归类为Value Obj。Value Obj应该是不可变的。

#### 5.3.1 设计Value Object
性能优化：多个相同的对象可指针引用到一个Value obj，而不必真实创建、管理多个对象。(插座例子，entity没有此优势)

value obj可以被复制和共享。哪个更合适取决于实现环境。复制可能导致系统被大量的对象阻塞，但共享可能会减慢分布式系统的速度。

Value Obj应设计为不可变的(通常规则)，以减少对变更的管理，极大地简化实现。但有些特殊情况，允许Value obj可变(如果value可变，就不能再共享它)。

#### 5.3.3 设计包含Value Object的关联
应尽量清除Value obj的双向关联。

同5.1，不必要的关联要消除。

### 5.4 模式：Service
有时，对象不是一个事物(物理实体)，比如活动或动作。有些操作从概念上讲不属于任何对象。Service用来表示此类对象，常以xxxManager之类的名字出现。

Service强调的是与其它对象的关系。好的service的三个特征：
1. 与领域概念相关的操作不是Entity或Value Obj的一个自然的部分； ？？
2. 接口是根据领域模型的其它元素定义的；  ？？
3. 操作是无状态的；（任何客户都可以时候用某个service的任何实例，而不必关心该实例的历史状态）

![总结](p90末尾黑体)

#### 5.4.1 Service与孤立的领域层
service可以划分到多个层，区分应用层service和领域层service；

#### 5.4.2 粒度
service其它作用：控制领域层中接口的粒度，避免客户与Entity和Value obj的耦合。

大型系统中，中等粒度的、无状态的service更容易被重用。

#### 5.4.3 对Service的访问
专用的service访问机制意义不大；一个“操作”对象可能足以作为service接口的实现。

### 5.5 模式：Module (也成为package)
传统的、较成熟的设计元素。Module之间应保持高内聚、低耦合。

#### 5.5.1 敏捷的Module
Module需要与模型的其它部分一同演变。

如果module有问题，与模型和代码不匹配了，需要同步重构module。

但也要尽力避免重构module，最大限度地减少与其他开发人员沟通时出现的混乱情况。

#### 5.5.2 基础设施驱动的打包存在的隐患
@ 分层架构下，打包太细会导致模型被割裂到多层，开发人员难以站在模型的角度去理解。
![两个代价](p96 末端)

除非真正有必要将代码分布到不同的服务器上，否则就把实现单一概念对象的所有代码放在同一个模块中（如果不能放在同一个对象中的话）。

利用打包把领域层从其他代码中分离出来。否则，就尽可能让领域开发人员自由地采用支持他们的模型和设计选择的方式来对领域对象进行打包。

@ 当前项目中的so既是打包，so太多了？？

### 5.6 建模模式(略)
（为何选择对象范式；例子给了不成熟范式造成的问题。）
#### 5.6.1 对象范式流行的原因
#### 5.6.2 对象世界中的非对象
#### 5.6.3 在混合范式中坚持使用Model-Driven Design

## Ch6：领域对象的生命周期
使用Factory创建和重建复杂对象，使用Aggregate来封装它们的内部结构；
最后，在生命周期的中间和末尾使用Repository来提供查找和检索持久对象并封装庞大基础设置的手段。

Factory和Repository在Aggregate基础上进行操作，将特定生命周期转换的复杂性封装起来。

Factory和Repository与Entity、Value obj和service不同，它不对应模型中的任何事物，而确实有承担领域层的部分职责。

### 6.1 模式：Aggregate
在具有复杂关联的模型中，要想保证对象更改的一致性是很苦难的。互不相联的对象要遵守一些固定规则，紧密关联的各组对象也要遵守一些固定规则。然而，过于谨慎的锁定机制又会导致多个用户之间毫无意义地互相干扰，从而使系统不可用。
因此，模型需要定义明确的边界及所属关系。

Aggregate是一组相关对象的集合，我们把它作为数据修改的单元。（删除person不能删除地址的例子）

每个Aggregate都有一个root和一个boundary（汽车与轮胎例子）：
- boundary定义了aggregate内部都有什么；边界内部的对象之间可以互相引用。
- root则是aggregate中所包含的一个特定entity； 根是aggregate中唯一允许外部对象保持对它的引用的元素。

固定规则：在数据变化时必须保持不变的一致性规则。Aggregate中的固定规则：7条。
总结为
![agg固定规则](p106 末端黑体)

purchase Order例子，合理划分Aggregate避免争用。

### 6.2 模式：Factory
- 例子：机械师装配发动机而不是另一种发动机组装配发动机，“装配复杂的复合对象的工作也最好与对象要执行的工作分开”。
- 客户负责创建对象时会看到对象的一些“固定规则”
鉴于以上两点，引入新的对象factory，factory是一种负责创建其它对象的程序元素。

![factory](p113 前端黑体)

好的Factory满足以下两个基本需求：
1. 每个创建方法都是原子方法，而且满足被创建对象或Aggregate的所有固定规则；
2. facotory应该被抽象为所需的类型，而不是创建出具体的类。

#### 6.2.1 选择Factory及其应用位置
“把factory用在那些需要隐藏细节的地方”。
可以在Aggregate的根上使用Factory method，也可以在一个对象上时候用Factory method。

#### 6.2.2 有些情况下只需要使用构造函数
以下情况最好使用简单的、公共的构造函数：
- 类是一种类型
- 。。。
5种场景

#### 6.2.3 接口的设计
- 每个操作都必须是原子的；
- Factory将与其参数发生耦合；

#### 6.2.4 固定规则的逻辑应放置在哪里
factory内部还是产品？

#### 6.2.5 Entity Factory与Value Object Factory

#### 6.2.6 重建已存储的对象
用于重建对象的factory与用于创建对象的factory很类似，主要由以下两点不同：
1. 用于重建对象的entity factory不分配新的跟踪ID；
2. 当固定规则未被满足时，重建对象的factory采用不同的处理方式。

### 6.3 模式：Repository
Factory封装了对象创建和重建时的生命周期转换。Repository封装对象和存储之间的互相转换。

把从已存储的数据中创建实例的过程称为“重建”。

过度使用数据库查询的问题：
![query](p121 前端黑体 + 后端黑体)

Repository用来封装数据库检索的解决方案，使我们的注意力重新回到模型上。
![repo](p122 中间段半示例性的，比黑体解释的好)

repo的优点：4点。

#### 6.3.1 Repository的查询
repo中的查询方式
- 硬编码方式查询；
- 基于specification的查询；

#### 6.3.2 开发人员不能忽略Repository的实现
数据库查询底层技术可能会限制我们的建模选择。

#### 6.3.3 Repository的实现
注意事项：
- 对类型进行抽象；
- 充分利用repo与客户解耦的优点；
- 将事物的控制权留给客户；

#### 6.3.4 在框架内工作
#### 6.3.5 Repository与Factory的关系
Factory负责处理对象生命周期的开始，而repo帮助管理生命周期的中间和结束。

Factory负责制造新对象，而repo负责查找已有对象。

### 6.4 为关系数据库设计对象


## Ch7：使用语言：一个拓展的示例
### 7.1 货物运输系统简介
### 7.2 隔离领域：应用程序的引入
### 7.3 将Entity和Value Object区别开
### 7.4 设计运输系统中的关联
### 7.5 Aggregate边界
### 7.6 选择Repository
### 7.7 场景走查
### 7.8 对象的创建
### 7.9 停下来重构：Cargo Aggregate的另一种设计
### 7.10 运输模型中的Module
### 7.11 引入新特性：配额检查
### 7.12 小结

## Ch14：保持模型的完整性
模型应保持内部的一致性。大型系统领域模型的完全统一是不可行的；但要通过有意识的设计决策保持模型关键部分的高度统一。
需标记出不同模型之间的边界和关系，以保证需统一的部分保持一致，不需要统一的部分不会引起混乱或破坏模型。

Bounded Context定义了每个模型的应用范围；
Context Map画出了上下文的范围，并给出了项目上下文以及它们之间关系的总体视图。

### 14.1 模式：Bounded Context
一个模型只在一个上下文中使用。这个上下文可以是代码的一个特定部分，也可以是某个特定团队的工作。

“明确地定义模型所应用的上下文。根据团队组织、软件系统的各部分用法及物理表现来设置模型的边界。在这些边界中严格保持模型的一致性，而不要收到边界之外问题的干扰和混淆。”

###### 识别Bounded Context中的不一致
模型中出现了差异的一个明显症状：已编码的接口不匹配；自动测试CI可以识别此类问题。

将不同模型的元素组合到一起可能引发的两类问题：重复的概念和假同源。
出现此类问题时，可能需重新对模型进行开发。

### 14.2 模式：Continous Integration
定义完一个Bounded Context后，必须让它保持合理化。

Continous Integration是指把一个上下文中的所有工作足够频繁地合并到一起，并使它们经常保持一致，以便当模型发生分裂时，可以迅速发现并纠正问题。CI的两个级别的操作：
1. 模型概念的集成；(团队成员之间沟通保证)
2. 实现的集成；

建立一个经常把所有代码和其他实现工件合并到一起的过程，并通过自动测试来快速查明模型的分裂问题。

### 14.3 模式：Context Map
只有一个Bounded Context并不能提供全局视图。其他模型的上下文可能仍不清楚而且还在不断变化。

- Context Map位于项目管理和软件设计之间的重叠区域。
- Context Map并不需要写成任何特殊形式的文档。
- Context Map始终表示他所处的情况（对context map的修改）。

###### Context Map的组织和文档化
1. Bounded Context应该有名称，以便可以讨论它们。名称应添加到团队ubiquitous language中。
2. 每个人都应知道边界在哪，且能够分辨出任何代码段，或任何情况的Context。（不同上下文的代码隔离到不同module中）

可以使用非正式的图，或严格的正式图，文本列表等表示概念边界。

### 14.4 Bounded Context之间的关系
14.5~14.11介绍的模式提供了把两个模型（处在两个bounded context中的）关联起来的各种策略。

|模式|简述|适用场景|
|--|--|--|
|Shared Kernel|从领域模型中选出两个团队都同意共享的一个子集(通常是Core domain；含模型和代码)；一个团队不应该单独擅自更改共享的内容，共享部分的CI频率比普通的低，两个团队都要运行测试。|团队或组织不能保持CI，或团队庞大、笨拙时|
|Customer/Supplier Development Team|两团队间建立明确的客户/供应商关系，下游团队作为上游的客户，根据下游需求协商任务预算；|子系统A的任务是服务于子系统B；或下游组件向上游反馈的信息很少，依赖是单向的；|
|Conformist（遵从者）|通过严格遵从上游团队的模型，消除在BC之间进行转换的复杂性；可极大地简化集成，与供应商团队共享一种LANG|不完美上下游关系，上游团队没有满足下游团队需求的动机；但仍依赖上游，上游质量可接受。|
|AntiCorruption Layer（防护层）|创建一个隔离的层，为客户提供符合其领域模型的功能；此层提供与另一个系统对话的接口，进行两个模型之间的双向转换。|不完美上下游关系，上游团队没有满足下游团队需求的动机；但仍依赖上游，上游设计难用，下游完全负责开发一个转换层。或新系统与遗留系统对接场景。|
|Separate Way（独立自主）|声明一个与其它上下文毫无关联的BC，使开发人员能在此小范围内找到简单、专用的解决方案|不完美上下游关系，上游团队没有满足下游团队需求的动机；下游完全放弃对上游的利用。或两组功能之间的关系并非必不可少，那么二者完全可以彼此独立|
|Open Host Service（开放主机服务）|定义一个协议，将子系统作为一组service供其它系统访问。开放此协议给其它系统集成，有新需求时拓展此协议；|一个子系统需与大量其它系统集成时，为每个集成都定制一个转换层效率低、维护难；|
|Published Language|把一个良好文档化的、能够表达出所需领域信息的共享语言作为公共的通信媒介(如XML)，必要时在其它信息与语言之间进行转换。|两个模型必须共存且必须交换信息时；不同企业之间需要互相交换信息时|

### 14.12 “大象”的统一
盲人摸象--》模型集成

Step1：弄清各部分是如何相连的；
Step2：去掉各个模型中那些偶然或不正确的方面，并创建新的概念。

### 14.13 选择你的模型上下文策略
绘制好Context map后，根据实际情况对其修改时，可以有意识地选择Context边界和关系；指导原则：
- 制定团队或更高层的决策
- 在上下文中工作
- 转换边界
- 接受无法更改的事务，描述外部系统
- 与外部系统的关系
- 正在设计的系统
- 满足不同模型的特殊需要
- 部署
- 权衡
- 项目正在进行时

### 14.14 转换
BC的变更
- 合并Context：Separate Way->Shared Kernel
- 合并Context：Shared Kernel->Continous Integration
- 逐步淘汰遗留系统
- Open Host Service->Published Language

## [书中提到的设计模式](design_pattern.md)

## 参考
1. Domain-Driven Design, Trakling Complexity in the Heart of Software; by Eric Evans.
2. [领域驱动设计到底难在哪？](https://www.jianshu.com/p/ab80cb9f307c)
3. [“领域驱动设计”答疑（汇总）](https://www.jianshu.com/p/f876d19a9aa3)
4. [DCI in C++](https://www.jianshu.com/p/bb9c35606d29)
