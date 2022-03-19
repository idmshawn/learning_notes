# Data Plane Telemetry (DTEL)基本概念
DTEL由以下三部分组成(三个部分可以不局限在一台switch中)：
- Watchlist：识别流量(Which flow to monitor)，一般使用SAI ACL实现，TCAM匹配报文头域段、端口等，AD指定telemetry动作；
- Event detection：事件监测，可监测三类事件：flow events、packet drop events、queue congestion events；
- Telemetry report：由监测事件触发，switch生成给monitor的telemetry报告，报告消息包含报文头和报文关联的switch metadata(如时间戳、上/下行端口、队列深度/时延)；

### DTEL的telemetry报告
- Flow Report
  - In-band Telemetry
  - Packet Postcard
- Drop report
- Queue Report



## 参考
1. [SAI-Proposal-Data-Plane-Telemetry.md](https://github.com/opencomputeproject/SAI/blob/master/doc/DTEL/SAI-Proposal-Data-Plane-Telemetry.md)
2. [Data-Plane-Telemetry-ONF-Connect-Public.pdf](https://opennetworking.org/wp-content/uploads/2018/12/Data-Plane-Telemetry-ONF-Connect-Public.pdf)
