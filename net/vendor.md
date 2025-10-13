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

## 思科AVC和NBAR2
[文档4]
#### AVC
Application Visibility and Controls (AVC) ，用于监控和管理应用性能指标；利用已有的NBAR2等技术，目标是适当地分类网络中的流量 
> "With this data, the network administrator can act on the classified traffic in order to properly prioritize and control flow through QoS policies."

相比传统的流机制NetFlow和Flexible NetFlow(FNF)，AVC主要使用五元组中的4个，即主要关注源/目的IP、协议号、目的端口，忽略源端口号，以便降低流数目、将多个类似流聚合为一条AVC流。
测量指标含(详见文档4)：
CND，Client Network Delay
SND，Server Network Delay，即WAN网络时延；
AD，Application Delay，应用处理时延；

#### NBAR 
Next Generation Network Based Application Recognition (NBAR2)，NBAR2为AVC提供了应用识别能力。
NBAR2基于其DPI(Deep Packet Inspection)引擎，提供了高级别的流量分类(providing a greater level of traffic classification)。
支持1000个应用签名，和不断更新的协议包，以更好地识别和基于Group匹配应用；如email组下的POP3、SMTP、IMAP等；

NBAR2测量对象含TCP、UDP，见文档4附图LiveNX Flow Report。

## 参考
1. CISCO Live: [Beginner’s Guide to ThousandEyes](https://www.ciscolive.com/c/dam/r/ciscolive/global-event/docs/2025/pdf/BRKENT-1656.pdf)
2. CISCO Live: [ThousandEyes: Assurance in Focus, A next generation platform for assuring digital experiences](https://www.ciscolive.com/c/dam/r/ciscolive/global-event/docs/2025/pdf/BRKOBS-1017.pdf)
3. [ThousandEyes + Cisco Catalyst 9000](https://www.thousandeyes.com/solutions/cisco-catalyst-9000-series)
4. 【推荐】[Cisco Application Visibility and Controls (AVC) and Next Generation NBAR (NBAR2)](https://docs.liveaction.com/pdf/Cisco%20AVC%20and%20NBAR2%20App%20Note.pdf)
5. [瞭解9800無線控制器上的應用可視性與可控性](https://www.cisco.com/c/zh_tw/support/docs/wireless/catalyst-9800-series-wireless-controllers/222242-understand-avc-on-the-catalyst-9800-wire.html)

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

# 行业洞察
[Cisco Live汇总](https://github.com/babajung/cisco-live/blob/master/README.md)

## IoA洞察
### 思科
思科旗下Outshift专注于IoA，于2025年7月份发布IoA白皮书，文档1。白皮书指出：

1、网络趋势从传统的Internet，到移动互联网，到云互联网，当前迎来了Agent互联网；网络基础设施需要有IoA的标准规范，以指导IoA基础设施的生态发展，避免碎片化发展、重复造轮子。   

2、给出Agent互联互通的两个例子：其它的SaaS指纹开发和管理、药物研发；    

3、定义了Multi-agent Software的三种模式：    
- Deterministic routing模式(Pattern 1)，适用于可靠性大于灵活性的企业关键任务处理；如，软件开发的流程中，agent用于安全扫描、依赖分析、容器执行顺序等。
- Semantic routing模式(Pattern 2)，适用于有限范围内灵活性的面向用户的系统；如，企业IT支撑中，用于解答数据库访问问题的“数据库代理”，诊断网络问题的“网络代理”。
- Planner-based模式(Pattern 3)，适用于灵活性最高的消费型应用；如，旅游规划代理，动态查找航班，酒店预订、天气服务等。

4、提供了[AGNTCY](https://github.com/agntcy/.github/blob/main/profile/README.md)开源工程，用于作为IoA的MAS(Multi-agent System)示范
The AGNTCY project is starting with deterministic patterns (Pattern 1) to establish reliable foundations, then expanding to semantic routing (Pattern 2), and eventually supporting planner-based systems (Pattern 3) as reasoning capabilities mature.

5、给出IoA定义：      
This new AI-native world needs a framework to enable collaboration across the ecosystem of agentic applications of various kinds, from different vendors, sometimes across different industries. **We call this framework the Internet of Agents.**

IoA需要内置量子安全。

6、IoA的构建，一般划分为三个互联层  
- AI-native agentic applications：这一层涵盖了从业务工作流程自动化到科学发现再到社交互动的全方位智能应用。
- **Agent Communication Platform (ACP)**：该层为AI代理如何发现、验证和相互交互提供了基本协议和标准。 （**瘦腰模型中IoA的“腰”**，相当于Internet中的“IP”，或Cloud Internet中的“HTTPS/gRPC/Open API”）
- AI and quantum-safe infrastructure：这一基础层提供了安全且可扩展的基础设施，支持所有AI代理的交互。


开源工程AGNTCY包含以下内容：

|项目|链接|作用|说明|
|--|--|--|--|
|Open Agent Schema Framework (OASF)|github.com/agntcy/oasf|提供标准格式的agent基础框架||
|Agent Connect Protocol (ACP)|github.com/agntcy/acp-spec|支持不同框架下的agent通信、处理认证、配置、错误处理的标准协议||
|Agent2Agent Protocol (A2A) by Google|a2a-protocol.org/latest/|agent间协同和通信的标准方式||
|Secure Low-latency Interactive Messaging (SLIM)|github.com/agntcy/slim||
|...|||
  
### 参考
1. 思科旗下Outshift的IoA白皮书：[The Internet of Agents](https://outshift-headless-cms-s3.s3.us-east-2.amazonaws.com/Internet_of_Agents_Whitepaper.pdf)
2. 多Agent系统(MAS, Multi-agent System)示例？，[AGNTCY](https://docs.agntcy.org/)

### 微软
人带领agent工作xxxxx

### 参考
1. [Microsoft Work Trend Index Annual Report](https://news.microsoft.com/annual-work-trend-index-2025/)

# 思科系统和软件汇总

|分类|工具/系统|全称|作用|备注|
|--|--|--|--|--|
|可视运维|千眼|ThousandEyes|运维可视系统|注2|
|可视运维|splunk||Unify network and application data for advanced observability and resilience. |收购的第三方公司？提供商业的可视解决方案；注7|
|安全|XDR|Extended Detection and Response|扩展的安全检测及响应系统，云原生SaaS|注6|
|安全|Umbrella||基于云的安全接入服务 (SASE)，提供 DNS 安全、SWG、CASB 等; Get flexible, fast, and effective cloud security so you can secure your users, even in a matter of minutes|注4|
|？|DNA Center|也称Cisco Catalyst Center|思科本地部署平台，防仿冒、终端识别基于DNAC。包含AI Endpoint Analytics，采用机器学习提升未知终端识别率，完成IoT设备的资产认证管控和资产可视化。||
|安全|ISE|Identity Services Engine|零信任架构下，ISE是策略决策点，统一认证、策略下发；It gathers intel from the stack to authenticate users and endpoints, automatically containing threats. Enable a dynamic and automated approach to policy enforcement|注1|
|安全|SNA，前称Stealthwatch|Secure Network Analytics|基于 NetFlow/Telemetry 做行为监测、威胁检测。Analyze your existing network data to help detect threats that may have found a way to bypass your existing controls, before they can do serious damage. Detect and respond to emerging threats in your digital business with industry-leading machine learning and behavioral modeling|注3，5，9|
|安全|SCA，前称Stealthwatch Cloud，后收编为NDR|Secure Cloud Analytics|云原生的流量分析平台，检测横向移动、可疑流量。||
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
