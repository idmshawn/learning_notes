
# IPFIX
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
