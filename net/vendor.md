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

| 序号 | 场景名称        | 行业/客户  | 关键场景描述                                                     | 参考链接                                                                                                                                                                                                                  |
| -- | ----------- | ------ | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | 全球连锁零售加密互联  | 大型零售集团 | 600 余家门店 C9300X 通过 IPsec 隧道直连 AWS，实现 POS 实时上云              | [Cisco 官方配置指南 - Catalyst 9000X IPsec 示例](https://www.cisco.com/c/zh_cn/support/docs/switches/catalyst-9300x-12y-a-switch/221564-configure-ipsec-on-catalyst-9000x-series.html)                                        |
| 2  | 欧洲机场安全回传    | 国际机场   | 航站楼 C9400X ↔ 云防火墙 IPsec 链路，承载离港/行李系统数据                     | [Cisco Catalyst 9000 Platform FAQ - 安全场景](https://www.cisco.com/c/en/us/products/collateral/switches/catalyst-9000/nb-06-cat9k-swit-plat-faq-cte-en.html)                                                             |
| 3  | 北美能源广域加密    | 能源公司   | 总部 C9400X 与 30 个野外变电站 C9300X 建立 Hub-Spoke IPsec 网络，替代 MPLS | [Cisco 官方配置指南 - Catalyst 9000X IPsec 示例](https://www.cisco.com/c/zh_cn/support/docs/switches/catalyst-9300x-12y-a-switch/221564-configure-ipsec-on-catalyst-9000x-series.html)                                        |
| 4  | 亚太制造混合云     | 制造企业   | 园区 C9300X IPsec 对接 AWS Transit Gateway，打通研发网与云上 DevOps     | [Cisco Security Configuration Guide - Catalyst 9300 IPsec](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9300/software/release/17-13/configuration_guide/sec/b_1713_sec_9300_cg/configuring_ipsec.html)  |
| 5  | 三甲医院多院区加密互联 | 医疗行业   | 主院区 C9400X 与两家分院 C9300X 建立 IPsec 隧道，承载 HIS/PACS 影像数据       | [Cisco Security Configuration Guide - Catalyst 9300 IPsec](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9300/software/release/17-13/configuration_guide/sec/b_1713_sec_9300_cg/configuring_ipsec.html)  |
| 6  | 金融机构分支零信任   | 银行/保险  | 分支 C9300X 通过 IPsec 与总部数据中心互联，实现瘦分支零信任架构                    | [Cisco Catalyst 9000 Platform FAQ - 安全场景](https://www.cisco.com/c/en/us/products/collateral/switches/catalyst-9000/nb-06-cat9k-swit-plat-faq-cte-en.html)                                                             |

# 公共

## 思科Flexible NetFlow



## 参考
1. [Flexible NetFlow](https://www.cisco.com/site/us/en/products/networking/software/ios-nx-os/flexible-netflow/index.html)
2. Datasheet [Cisco IOS Flexible NetFlow](https://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/flexible-netflow/product_data_sheet0900aecd804b590b.html)

## 其它
[Cisco Live汇总](https://github.com/babajung/cisco-live/blob/master/README.md)
