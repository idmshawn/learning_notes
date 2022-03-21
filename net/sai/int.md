# Inband Telemetry

## INT(Inband Network Telemetry)
Barefoot及P4.org于2015年提出INT规范，Alibaba, Arista, CableLabs, Cisco Systems, Dell, Intel, Marvell, Netronome, VMware等公司均有贡献。最新版2.1标准2020-11-11发布。  
Barefoot的SPRINT(**S**mart、**P**rogrammable、**R**eal Time **INT**)解决方案：转发面与SDK软件结合的，针对白盒生态系统的解决方案；转发面使用P4实现可编程，SDK适配SAI的DTEL。


### 参考
1. [In-band Network Telemetry (INT) Dataplane Specification](https://p4.org/p4-spec/docs/INT_v2_1.pdf)
2. [In-band Network Telemetry (INT)](https://nkatta.github.io/papers/int-hula.pdf)
3. [Improving Network Monitoring and Management with Programmable Data Planes](https://opennetworking.org/news-and-events/blog/improving-network-monitoring-and-management-with-programmable-data-planes/)

## iOAM(In-Situ OAM)
Cisco联合Facebook、Mellanox、Marvell、Barefoot于2016.11提交INT的IETF草案，后更名为In-situ OAM；  

### 参考
1. [CiscoDevNet/iOAM](https://github.com/CiscoDevNet/iOAM)


## IFA(Inband Flow Analyzer)
2018年提出，Broadcom, Arista, Alibaba, Huawei, Fujian Ruijie等公司参与贡献。最新版至2022年。

实现原理类似INT：
- IFA delivers Inband Telemetry;
- Each hop adds its metadata to the user packet in the dataplane;
- Metadata is gathered from each node in a cumulative manner;
- Last network node removes the metadata and sends one consolidated report to the collector application;

### 参考
1. [IFA的IETF草案](https://datatracker.ietf.org/doc/draft-kumar-ippm-ifa/)
2. [Inband Flow Analyzer (IFA) 2.0 Probe for Real-Time Flow Monitoring](https://www.juniper.net/documentation/us/en/software/junos/flow-monitoring/topics/topic-map/ifa2.0-probe-for-real-time-performance-monitoring.html)
3. [Trident 4 IFA 2.0 w/ BroadView Instrumentation & AIOps](https://www.broadcom.com/video/eb1489a0ce8e428797dfb4342366184a)

## iFIT(In-situ Flow Information Telemetry)
华为及中国移动于2018年提出的in-band telemtry方案。支持逐包的高精度监测。  
上报方式为Postcard模式，而非INT、IFA和iOAM的stack metadata形式(或称Passport模式)。

### 参考
1. [In-situ Flow Information Telemetry Framework](https://tools.ietf.org/id/draft-song-opsawg-ifit-framework-00.html)
2. [（IPv6+系列电子书）IFIT](https://support.huawei.com/enterprise/zh/doc/EDOC1100195086?idPath=24030814%7C9856750%7C22715517%7C23708778%7C252772223)
