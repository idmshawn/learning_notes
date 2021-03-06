
## 基本概念
### 桥接(Bridging)
##### .1D Bridging
IEEE 802.1D提出MAC bridge标准，**桥接(Ethernet bridging)是基于MAC地址的二层(数据链路层)转发**，基本操作含：  
- 泛洪(Flooding)：是交换机和网桥使用的一种数据流传递技术，将某个接口收到的数据流从除该接口之外的所有接口发送出去。[泛洪和广播的区别](https://blog.51cto.com/tingfeng/795612)：泛洪操作广播的是普通数据帧而不是广播帧。
- 转发(Forwarding)
- 学习(Learning)

##### .1Q VLAN
IEEE 802.1Q在.1D的基础上扩展，引入VLAN；VLAN对物理以太网做了逻辑划分：
- 报文仅在单个VLAN内桥接；
- 带有未知DA或广播DA的报文仅在VLAN内泛洪；

##### .1P priority
IEEE 802.1P在.1Q的基础上扩展，引入“priority tagged”，仅传输优先级、不传输VID；  

桥接图示[见文档4]  
![brg](../images/bridge.png)  


### 交换(Switching)

桥接是连接两个不同的物理网段(冲突域)的技术，分隔冲突域，根据MAC地址来判断连接两个物理网段的计算机的数据包发送。     
交换也是以MAC地址作为判断依据来将网络划分成两个不同段的技术。不同的是，交换将物理网段划分到每一个端口当中，简单的理解就是一种多端口的网桥，它实际上是一种桥接技术的延伸，交换机每个端口实际上就是一个网桥。  

交换图示[见文档4]  
![sw](../images/switch.png)    

### 路由(Routing)

## 桥接/交换的区别
在判断数据的时候，**网桥只能判断是否在同一个物理网段，交换机则可以判断数据包是属于哪一个端口**。

### 二层交换机与网桥的区别
网桥（Bridge），也叫桥接器，是早期的两端口二层网络设备，用来连接不同网段。网桥的两个端口分别有一条独立的交换信道，不是共享一条背板总线，可隔离冲突域。网桥比集线器（Hub）性能更好，集线器上各端口都是共享同一条背板总线的。后来，网桥被具有更多端口、同时也可隔离冲突域的交换机（Switch）所取代。

网桥与交换机的区别在与市场，而不在与技术。交换机对网络进行分段的方式与网桥相同，交换机就是一个多端口的网桥。确切地说，**高端口密度的网桥就称为局域网交换机**。   
交换机与网桥的真正区别主要在与现代的交换机与旧式网桥的区别上。   
两者在网络中的位置见文档2。  

局域网交换机的基本功能与网桥一样，具有帧转发、帧过滤和生成树算法功能。但是，交换机与网桥相比还是存在以下不同：   
1. 交换机工作时，实际上允许许多组端口间的通道同时工作。所以，交换机的功能体现出不仅仅是一个网桥的功能，而是多个网桥功能的集合。即**网桥一般分有两个端口，而交换机具有高密度的端口**。 
2. 分段能力的区别   
  由于交换机能够支持多个端口，因此可以把网络系统划分成为更多的物理网段，这样使得整个网络系统具有更高的带宽。而网桥仅仅支持两个端口，所以，网桥划分的物理网段是相当有限的。 
3. 传输速率的区别  
　交换机与网桥数据信息的传输速率相比，交换机要快于网桥。 
4. 数据帧转发方式的区别  
　网桥在发送数据帧前，通常要接收到完整的数据帧并执行帧检测序列FCS后，才开始转发该数据帧。交换机具有存储转发和直接转发两种帧转发方式。直接转发方式在发送数据以前，不需要在接收完整个数据帧和经过32bit循环冗余校验码CRC的计算检查后的等待时间。
5. 生成树实例的不同  
　对于网桥来说，一个网桥就只有一个生成树实例。而对于交换机来说，一个交换机往往对应着多个生成树实例。  
  生成树协议用于阻止在第二层网络上产生网路环路。协议监视网络中所有可用的链路，并在必要的时候关闭任何冗余的接口来确保在网络中不会发生任何的环路。生成树算法会创建一个拓扑数据库，然后搜索并破坏掉冗余的链路。如果不能够有效的阻止网络环路的话，就会遇到广播风暴、多帧复制等问题。

## 网络设备

|工作层|设备|英文|传输对象|功能|功能详述|作用场景|
|--|--|--|--|--|--|--|
|物理层|中继器|Repeator?|比特流|连接、放大|连接同一个网络的两个或多个网段，完成信号的复制、调整和放大|增加信号传输的距离，延长网络长度和覆盖区域|
|物理层|集线器|Hub|比特流|共享型设备|把一些机器连接起来组成局域网-星型连接拓扑|通过广播的方式共享带宽；带宽利用低，广播风暴泛滥，效率低下|
|数据链路层|网桥|Bridge|以太网帧头|桥接、重发器|桥接和隔离两个网段，延长线路距离、信号再生和转发|适合联接数量不多的、同一类型的网段[注1]|
|数据链路层|二层交换机|L2 Switch|以太网帧头|同一网络中主机的通讯，过滤|物理隔离网段（MAC地址）||
|网络层|三层交换机|L3 Switch|以太网帧头|不同Vlan的主机通讯||接口类型简单，拥有很强二层包处理能力，端口之间可进行快速交换，适用于大型局域网|
|网络层|路由器|Router|IP数据包|不同网络间的互联，路由|逻辑隔离网段并找到网段中最合适的路径（IP地址）|单播，路由器屏蔽了物理网络的特征，实现跨网段转发|
|传输层以上|网关|Gateway||网间连接器、协议转换器|不同协议之间的转换，实现不同协议网络间的互连|广域网互连/局域网互连|

注：
1. 除了隔离冲突域以外，网桥还可以实现不同类型网络的连接(令牌环网和以太网之间的连接)和网络的拓展(IEEE的5.4.3连接规则)等功能。[见文档4]

## 参考
1. [网桥与交换机的区别](https://blog.csdn.net/fivedoumi/article/details/51746798)
2. [集线器、网桥、交换机的区别](https://blog.csdn.net/dwj_daiwenjie/article/details/108636144)
3. [桥接、交换和路由的区别](README.md)
4. [教你全面认识网络桥接、交换和路由](https://www.docin.com/p-2253823700.html)
