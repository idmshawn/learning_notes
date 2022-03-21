
# Telementry
Telementry、INT、DTEL、TAM的区别？
- Telementry：运维标准及协议；
- in-band telemetry：在转发路径设备的报文中插入metadata数据或in-band telemtry报文头，终点设备再剥掉metadata及报文头，并将相关信息上报monitor[见文档1]；  
in-band telemetry和postcard的区别见DTEL中的例子[见文档2]；  
常见的in-band telemtry标准协议含以下几种：
  - [INT](int.md)：In-band Network Telemetry，P4.org于2015年提出；
  - [IFA](https://datatracker.ietf.org/doc/draft-kumar-ippm-ifa/)；
  - [IOAM](https://github.com/CiscoDevNet/iOAM)，IETF于2019年提出；  
- [DTEL](dtel.md)：Data Plane Telemetry，Barefoot于2017年提出的数据面telementry适配方案，SAI支持DTEL相关API；
- [TAM](tam.md)：SAI Telemetry and Monitoring，Broadcom于2017年提出的数据面telementry适配方案，SAI支持TAM相关API；

## 参考
1. TELEMETRY AND MONITORING 2.0 PROPOSAL DISCUSSION OCP SAI；
2. SAI-Proposal-Data-Plane-Telemetry.md
