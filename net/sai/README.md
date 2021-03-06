
# Telementry
Telementry：运维标准及协议；完整的Telementry实现涵盖管理面(Management Plane)、控制面(Control Plane)和数据面(Data Plane)。
![image](https://user-images.githubusercontent.com/61963619/159226989-2ec8f512-4828-47af-b6af-c0b9e9e1188c.png)

Telementry、INT、DTEL、TAM的区别？
## Inband Telemetry
在转发路径设备的报文中插入metadata数据或in-band telemtry报文头，路径上的每个设备节点都将自己的metadata信息依次插入到报文中，终点设备再统一剥掉metadata及报文头，并将相关信息上报monitor[见文档1]；  

INT vs. Postcard，或见DTEL中的例子[见文档2]；  
- INT: Event detect on sink node 
  - Stack metadata according to instruction hop by hop
  - Drop events needs special handling   
- Postcard: Event detect on each node 
  - Trigger report as a mirrored packet on each hop
  - Analyzer needs additional steps to correlate mirrored packet of same flow acress multiple hops.

常见的[Inband Telemetry](int.md)标准含以下几种：
|标准|全称|主导厂商|提出时间|最后更新时间|Collector(Monitor)端软件|
|--|--|--|--|--|--|
|INT|Inband Network Telemetry|Barefoot|2015|2020.11|Deep Insight Analytics|
|iOAM|Inband OAM，后更名为In-situ OAM|Cisco|2016.11||Tetration Analytics|
|IFA|Inband Flow Analyzer|BroadComm|2018|2022|AIOps|
|iFIT|In-situ Flow Information Telemetry|Huawei|2018||iMaster NCE|

## Data Plane Telemetry
Telemetry的管理面、控制面实现一般由OTT厂商或运营商实现；芯片厂商提供数据面的物理芯片和SDK软件，主要关心数据面Telemetry，提供部分控制面支持。  
不同的芯片厂商主推根据各自的数据面Telementry实现，SAI上主要支持了博通的TAM和Barefoot的DTEL：
- [DTEL](dtel.md)：Data Plane Telemetry，Barefoot于2017年提出的数据面telementry适配方案，SAI支持DTEL相关API；支持INT。
- [TAM](tam.md)：SAI Telemetry and Monitoring，Broadcom于2017年提出的数据面telementry适配方案，SAI支持TAM相关API；支持INT、IFA、IPFIX？、sFlow等。
- [NetFlow(IPFIX)](ipfix.md)：IETF标准，基于思科2016提出的NetFlow v9，早期技术，只能基于流做telemetry；
- [sFlow](ipfix.md)：早期技术，流采样；SAI的`sai_tam_report_type_t`支持IPFIX和sFlow；

## 参考
1. TELEMETRY AND MONITORING 2.0 PROPOSAL DISCUSSION OCP SAI；
2. SAI-Proposal-Data-Plane-Telemetry.md
