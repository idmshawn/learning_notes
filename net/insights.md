# 网络技术洞察

## 知识库

#### 白盒软件架构
- [SAI介绍(推荐)](https://www.design-reuse.com/articles/44519/switch-abstraction-interface-sai.html)

#### Software for Open Networking in the Cloud(SONiC)
- [Sonic官网](https://azure.github.io/SONiC/)
- SONiC架构
 - [SONiC软件组成](sonic.md)
 - [官网Wiki](https://github.com/Azure/SONiC/wiki/Architecture)
 - [SONIC架构简要分析-数据库](https://blog.csdn.net/armlinuxww/article/details/97236788)
- 内部资料
数据通信/vFast/Docs/转发芯片SDK业务主干/05.DPFC/01.技术管理/01.架构/sonic初步分析.pptx

#### Switch Abstraction Interface(SAI)
微码等厂商发起的白盒交换机转发适配API，2015年作为OCP开源项目，apache许可；
- [OCP官网SAI介绍](https://www.opencompute.org/wiki/Networking/SAI)
- SAI文档
代码库doc目录下对应特性文档帮助理解SAI接口
- **[SAI知识汇总](sai/README.md)**

#### 其它
- Open Compute Project(OCP) [官网](https://www.opencompute.org/)
SAI和SONiC为OCP Networking领域的两个开源子项目；

- DANOS(The Disaggregated Network Operating System) [官网](https://www.danosproject.org/)
起源于AT&T的“dNOS”项目，白盒设备使用的NOS, 2018年作为linux基金会开源项目，GPLv2许可；

- FAL(Forwarding Abstraction Layer)
摘自DANOS白皮书：
dNOS includes a set of components to support multiple different forwarding layers. A
forwarding abstraction layer (FAL) is responsible for taking high-level network state input from the shared infrastructure and data components and translating into vendor specific APIs for various software and hardware forwarding options.

## 代码库

###### SONiC(开源)
- [SONiC主库](https://github.com/Azure/sonic-buildimage)   
主库，不需要下载，下载SWSS即可；   
[介绍](https://github.com/Azure/SONiC/blob/master/sourcecode.md)了SONiC主库及其子库的功能定位及链接；

- [SONiC的SWSS模块](https://github.com/Azure/sonic-swss)  
调用SAI的多在orchagent目录

###### SAI(开源)
- [主库](https://github.com/opencomputeproject/SAI)  
关注inc下的头文件和doc下文档即可，无子库

###### BCM代码
- [BCM的SAI适配(开源)](https://github.com/Broadcom-Switch/SAI/releases)  
- [BCM OpenNSL(开源)](https://github.com/Broadcom-Switch/OpenNSL)  
[API手册](http://broadcom-switch.github.io/OpenNSL/doc/html/index.html)

###### Mellanox代码
- [Mellanox的SAI适配(开源)](https://github.com/Mellanox/SAI-Implementation)
