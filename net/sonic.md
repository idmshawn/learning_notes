## SONiC架构
SONiC是微软自研的NOS，2016年开源；SONiC定位是网络软件集合，不是Linux的发行版本；  
![image.png](https://.../image.png)

官网给出的SONiC架构图  
![sonic](../images/sonic.jpg)

## SONiC软件组成
SWSS(Switch State Service)包含了orchagent(Orchestration agent)、DB及syncd等多个子模块。
对于SAI开发者，主要关注orchagent、syncd和ASIC DB。
SWSS的子模块部署在三个不同的容器下，见前文架构图。  
![image.png](https://../image.png)

#### DB容器(database container)
见官网解释，**SAI需实现的ASIC_DB?**  

#### SwSS容器(swss container)
SwSS容器中包含两部分
###### \*syncd
用于支持SONiC应用和SONiC中心化消息基础设置(redis DB)之间的连接通信；（属于一种数据同步中间件？）
如上图，lldp,fpm, team是在各自业务的容器里， port、intf和neigh是在SwSS容器中。  

###### orchagent及\*mgrd
SwSS中的\*syncd程序可以看做信息往DB中的注入者/提供者，以下程序则是信息的消费者：
- **Orchagent**：SwSS的最关键组件，其中的处理逻辑支持提取所有\*syncd程序的注入状态，并根据这些状态做出进一步处理，下发到南向接口(ASIC_DB)。
SwSS内部会有一到多个Orchestration agent，它们负责APP_DB（网络应用操作表项对象）到ASIC_DB（转发芯片硬件表项对象）进行转换。Orchagent可以见到ADDL_DB和ASIC DB两个数据库，是APPL_DB的消费者，同时又是ASIC_DB的生产者。

- \*mgrd：根据APPL_DB, CONFIG_DB and STATE_DB的状态配置内核的Interface(intfMgrd)或Vlan interface(VlanMgrd).

#### synd容器(syncd container)
syncd提供一种机制，用于switch网络状态和swtich真实硬件/芯片之间的同步，含初始化、配置以及ASIC实时状态的收集等。
- **syncd**：实现上述的同步处理；syncd编译时链接ASIC SDK库。
“同步”：syncd订阅ASIC_DB以感知SwSS动作并通过SAI下发到硬件，同时也作为硬件状态的生产者。
- SAI API：
- ASIC SDK：由各厂商以动态链接库形式提供，实现SAI形式标准接口。
