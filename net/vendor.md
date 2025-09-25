[TOC]

# 网络可视

## 思科千眼
思科的网络可视用户端：通过可视网络，显著降低问题定位时间，目标“decreases your mean-time-to-resolution & mean-time-to-innocence”。
从终端、网络设备、云服务商主动收集数据，生成同步流量。（千眼客户端代理可以安装在云服务商、思科网络设备和电脑中）

1990年代的“Traceroute”相当于哈勃望远镜，2020年代发布的“千眼”相当于James Webb望远镜。

按文档1、2，“千眼”解决“确定性(Assurance)”、“可观察性(Observability)”问题，其功能包含：
- 网络拓扑跟踪；
- 应用质量查看；
- 网络链路质量查看；

## 思科splunk


## 华为NCE-CampusInsight

## 参考
1. CISCO Live: [Beginner’s Guide to ThousandEyes](https://www.ciscolive.com/c/dam/r/ciscolive/global-event/docs/2025/pdf/BRKENT-1656.pdf)
2. CISCO Live: [ThousandEyes: Assurance in Focus, A next generation platform for assuring digital experiences](https://www.ciscolive.com/c/dam/r/ciscolive/global-event/docs/2025/pdf/BRKOBS-1017.pdf)
3. [ThousandEyes + Cisco Catalyst 9000](https://www.thousandeyes.com/solutions/cisco-catalyst-9000-series)

# 网络安全

## 思科IPSec
思科C9000系列IPSec商用案例(数据来自Kimi搜索)  --》 数据参考源都不对

## ETA
Encrypted Traffic Analytics is an IOS XE feature that uses advanced behavioral algorithms to identify malicious traffic patterns through analysis of intraflow metadata of encrypted traffic, detecting potential threats hiding in encrypted traffic. 

加密流量不能应用DPI(deep-packet inspection).
Encrypted Traffic Analytics (ETA) is a unique capability for identifying malware in encrypted traffic coming from the **access layer**. Since more and more traffic is becoming encrypted, the visibility this feature affords for threat detection is critical for keeping your network secure at different layers.

Encrypted Traffic Analytics (ETA): You benefit from the power of machine learning to identify and take actions toward threats or anomalies in your network, including malware detection in encrypted traffic (without decryption) and distributed anomaly detection.

ETA extracts two main data elements: the **initial data packet (IDP)** and the **sequence of packet length and time** (SPLT). These elements are then communicated using a dedicated NetFlow template to Cisco Stealthwatch Enterprise. When used in conjunction with Flexible NetFlow, a complete view of the life of the flow is possible providing the capability to not only identify malicious traffic but anomalous behavior and customizable policy violations in your network utilizing.

思科的云端使用机器学习(ML)算法：
Cisco Stealthwatch with Cognitive Intelligence uses machine-learning algorithms. The training period allows the system to learn the behavior of the customer network. The length of the training period depends entirely on the amount of traffic seen. Once this initial period is complete, Cognitive Intelligence analyzes the encrypted traffic data elements within the ETA records by applying machine learning and statistical modeling with existing classifiers.

### 应用场景
思科[文档1]列举了
1.  医疗场景 Figure 6 Encrypted medical communications in Cisco SD-Access fabric。
2.  零售场景 Figure 13 Addition of ETA in retail network

### 参考
1. [Encrypted Traffic Analytics: Solutions Adoption Prescriptive Reference—Design Guide](https://www.cisco.com/c/dam/en/us/td/docs/solutions/CVD/Campus/eta-design-guide-2019oct.pdf?dtid=osscdc000283&linkclickid=srch) 2019.


## TrustSec策略可视

### 参考
1. [TrustSec Refresh, Reinforced with latest segmentation innovations](https://www.ciscolive.com/c/dam/r/ciscolive/global-event/docs/2024/pdf/BRKENS-1852.pdf)

# 行业洞察(其它)
[Cisco Live汇总](https://github.com/babajung/cisco-live/blob/master/README.md)

# 思科系统和软件汇总

|分类|工具/系统|全称|作用|备注|
|--|--|--|--|--|
|可视运维|千眼|ThousandEyes|运维可视系统|注2|
|可视运维|splunk||Unify network and application data for advanced observability and resilience. |收购的第三方公司？提供商业的可视解决方案；注7|
|安全|XDR|Extended Detection and Response|安全检测及响应系统|注6|
|安全|Umbrella||基于云的安全接入服务 (SASE)，提供 DNS 安全、SWG、CASB 等; Get flexible, fast, and effective cloud security so you can secure your users, even in a matter of minutes|注4|
|？|DNA Center|也称Cisco Catalyst Center|思科本地部署平台，防仿冒、终端识别基于DNAC||
|安全|ISE|Identity Services Engine|零信任架构下，ISE是策略决策点，统一认证、策略下发；It gathers intel from the stack to authenticate users and endpoints, automatically containing threats. Enable a dynamic and automated approach to policy enforcement|注1|
|安全|SNA，前称Stealthwatch|Secure Network Analytics|基于 NetFlow/Telemetry 做行为监测、威胁检测。Analyze your existing network data to help detect threats that may have found a way to bypass your existing controls, before they can do serious damage. Detect and respond to emerging threats in your digital business with industry-leading machine learning and behavioral modeling|注3，5，9|
|安全|SCA，前称Stealthwatch Cloud|Secure Cloud Analytics|云原生的流量分析平台，检测横向移动、可疑流量。||
|？|Meraki||Secure and manage IT from an intuitive, cloud-based dashboard with built-in assurance. |注8|
|安全|Duo||提供 MFA 与零信任身份校验，收购公司||
|AI|OutShift||专注于Internet of Agents，思科旗下公司|注10|
|安全|Hypershield||下一代分布式安全架构，把安全能力嵌入交换机、服务器网卡、虚拟化层，实现“AI 原生 + 无处不在的防御”|注11|

Secure Network Analytics 可以快速、准确地检测到威胁（例如网络命令-与-控制 (C&C) 攻击、勒索软件、分布式拒绝服务 (DDoS) 攻击、非法加密货币挖矿、未知恶意软件和内部威胁）。通过使用无代理解决方案，您可以对整个网络流量进行全面的威胁监控，即使流量已加密也是如此。

## 参考
1. [Cisco Identity Services Engine (ISE)](https://www.cisco.com/site/us/en/products/security/identity-services-engine/index.html)
2. [Cisco ThousandEyes](https://www.cisco.com/site/us/en/products/networking/software/internet-cloud-intelligence/index.html)
3. [Cisco Secure Network Analytics](https://www.cisco.com/site/us/en/products/security/security-analytics/secure-network-analytics/index.html)
4. [Cisco Umbrella](https://umbrella.cisco.com/)
5. [Network threat detection and response with Cisco Stealthwatch](https://www.cisco.com/site/us/en/products/security/security-analytics/secure-network-analytics/index.html)
6. [Cisco XDR](https://www.cisco.com/site/us/en/products/security/xdr/index.html)
7. [splunk](https://www.splunk.com/en_us/products/observability.html)
8. [meraki: CLOUD-MANAGED NETWORK MANAGEMENT](https://meraki.cisco.com/products/meraki-dashboard/)
9. [Cisco Secure Network Analytics](https://www.cisco.com/c/zh_cn/products/collateral/security/stealthwatch/datasheet-c78-739398.html)
10. [outshift](https://outshift.cisco.com/the-internet-of-agents)
11. [Cisco Hypershield](https://www.cisco.com/site/us/en/products/security/hypershield/index.html)
