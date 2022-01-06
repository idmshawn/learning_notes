# 网络技术洞察

## 网络操作系统

### SONiC(Software for Open Networking in the Cloud)
- [Sonic官网](https://azure.github.io/SONiC/)
- SONiC架构  
  - [SONiC软件组成](sonic.md)
  - [官网Wiki](https://github.com/Azure/SONiC/wiki/Architecture)
  - [SONIC架构简要分析-数据库](https://blog.csdn.net/armlinuxww/article/details/97236788)

###### SONiC开源代码
- [SONiC主库](https://github.com/Azure/sonic-buildimage)   
主库，不需要下载，下载SWSS即可；   
[介绍](https://github.com/Azure/SONiC/blob/master/sourcecode.md)了SONiC主库及其子库的功能定位及链接；
- [SONiC的SWSS模块](https://github.com/Azure/sonic-swss)  
调用SAI的多在orchagent目录

### DANOS(The Disaggregated Network Operating System) 
起源于AT&T的“dNOS”项目，白盒设备使用的NOS, 2018年作为linux基金会开源项目，GPLv2许可；
- [官网](https://www.danosproject.org/)

### CNOS(China Network Operating System)/司络
- [发布新闻](https://baijiahao.baidu.com/s?id=1633476066483442179&wfr=spider&for=pc)  
- [CNOS（司络）- 中国网络操作系统：部分展示](https://www.zcool.com.cn/work/ZNDYyMTg1NjQ=.html)

## 网络抽象层

### SAI(Switch Abstraction Interface)
微码等厂商发起的白盒交换机转发适配API，2015年作为OCP开源项目，apache许可；
- [OCP官网SAI介绍](https://www.opencompute.org/wiki/Networking/SAI)
- [SAI介绍(推荐)](https://www.design-reuse.com/articles/44519/switch-abstraction-interface-sai.html)
- SAI文档
代码库doc目录下对应特性文档帮助理解SAI接口
- **[SAI知识汇总](sai/README.md)**

###### SAI开源代码
- [SAI主库](https://github.com/opencomputeproject/SAI)  
关注inc下的头文件和doc下文档即可，无子库

###### BCM适配SAI代码
- [BCM的SAI适配(开源)](https://github.com/Broadcom-Switch/SAI/releases)  
- [BCM OpenNSL(开源)](https://github.com/Broadcom-Switch/OpenNSL)  
[API手册](http://broadcom-switch.github.io/OpenNSL/doc/html/index.html)

###### Mellanox适配SAI代码
- [Mellanox的SAI适配(开源)](https://github.com/Mellanox/SAI-Implementation)

### FAL(Forwarding Abstraction Layer)
摘自DANOS白皮书：  
dNOS includes a set of components to support multiple different forwarding layers. A
forwarding abstraction layer (FAL) is responsible for taking high-level network state input from the shared infrastructure and data components and translating into vendor specific APIs for various software and hardware forwarding options.

## 网络组织或联盟
- [OCP(Open Compute Project)](https://www.opencompute.org/)  
SAI和SONiC为OCP Networking领域的两个开源子项目；

- [ONF(Open Networking Foundation)](https://opennetworking.org/)  
ONF的SDN基础设施包括ONOS(Open Network Operating System)和Stratum两种开源网络操作系统。

- 未来网络xx联盟

