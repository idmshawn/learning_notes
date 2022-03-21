
# IPFIX
即Cisco NetFlow Version9。  
将报文根据特性或fingerprint划分成流，针对流生成meta-data，发给collector。  
NetFlow v9基于模板设置可视信息，灵活性较高。   
支持正常NetFlow和采样NetFlow两种模式。

# sFlow
高度依赖统计采样，输出报文头给collector。报文头由预设的报文字节，或Eth、IPv4帧组成。
