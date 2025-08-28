
# NetFlow(IPFIX)
即Cisco NetFlow Version9。  
将报文根据特性或fingerprint划分成流，针对流生成meta-data，发给collector。  
NetFlow v9基于模板设置可视信息，灵活性较高。   
支持正常NetFlow和采样NetFlow两种模式。

# sFlow
高度依赖统计采样，输出报文头给collector。报文头由预设的报文字节，或Eth、IPv4帧组成。

# FlowCache模块
思科芯片的下一代数据面telemtry技术，ASIC芯片中有一个名为FlowCache的模块，可以支持逐包的、无需采样的telemtry，支持event机制。  
直接由ASIC生成metadata数据，对控制面无影响，避免CPU瓶颈和软件性能问题。

思科同步提供了Collector客户端。但对SAI的支持较弱？？

# 参考
1. DC Flow Telemetry - Features Comparison - Cisco Cloud Scale ASICs & Merchant ASICs - White Paper.pdf

# 思科Flexible NetFlow
思科Flexible NetFlow的概念在2012年就有，并非新东西；[文档2]的datasheet手册是2006年更新的，最后一次更新2008年。

Datasheet中两次提到，Flexible NetFlow是思科IOS软件的一个重要部分。即，Flexible NetFlow是完全通过软件实现的？？ 是不是Netstream中的灵活流上报？？
Flexible NetFlow is integral part of Cisco IOS Software that collects and measures data allowing all routers or switches in the network to become a source of telemetry and a monitoring device. Flexible NetFlow allows extremely granular and accurate traffic measurements and high-level aggregated traffic collection. Because it is part of Cisco IOS Software, Flexible NetFlow enables Cisco product-based networks to perform traffic flow analysis without purchasing external probes--making traffic analysis economical on large IP networks.

## 参考
1. [Flexible NetFlow](https://www.cisco.com/site/us/en/products/networking/software/ios-nx-os/flexible-netflow/index.html)
2. Datasheet [Cisco IOS Flexible NetFlow](https://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/flexible-netflow/product_data_sheet0900aecd804b590b.html)
