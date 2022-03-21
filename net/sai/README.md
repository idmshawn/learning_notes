
# Telementry
Telementry：运维标准及协议；完成的Telementry实现涵盖管理面、控制面(Control Plane)和数据面(Data Plane)。

Telementry、INT、DTEL、TAM的区别？
### Inband Telemetry
在转发路径设备的报文中插入metadata数据或in-band telemtry报文头，路径上的每个设备节点都将自己的metadata信息依次插入到报文中，终点设备再统一剥掉metadata及报文头，并将相关信息上报monitor[见文档1]；  
Inband Telemetry和postcard的区别见DTEL中的例子[见文档2]；  
常见的Inband Telemetry标准含以下几种：
- [INT](int.md)：In-band Network Telemetry，P4.org于2015年提出；
- [IFA](https://datatracker.ietf.org/doc/draft-kumar-ippm-ifa/)；
- [IOAM](https://github.com/CiscoDevNet/iOAM)，IETF于2019年提出；  

### Data Plane Telemetry
不同的厂商主推根据各自芯片实现的数据面Telementry，SAI上主要支持了TAM和DTEL：
- [DTEL](dtel.md)：Data Plane Telemetry，Barefoot于2017年提出的数据面telementry适配方案，SAI支持DTEL相关API；
- [TAM](tam.md)：SAI Telemetry and Monitoring，Broadcom于2017年提出的数据面telementry适配方案，SAI支持TAM相关API；

## 参考
1. TELEMETRY AND MONITORING 2.0 PROPOSAL DISCUSSION OCP SAI；
2. SAI-Proposal-Data-Plane-Telemetry.md
