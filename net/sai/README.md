# 基本概念

Telementry、INT、DTEL、TAM的区别？
- Telementry：运维标准？
- INT：Inband Network Telemetry，
- DTEL：Data Plane Telemetry，SAI提出？
- TAM：SAI Telemetry and Monitoring (TAM)，SAI提出；

# TAM
[源文档](https://github.com/opencomputeproject/SAI/tree/master/doc/TAM)

## 数据模型
#### 数据获取模型
- Push：发布(publish)/订阅(subscribe)机制；
- Pull：仍存在通过pull立即显示数据的需求。SAI提供一个API支持多种不同的数据。

```c
/**
 * @brief TAM telemetry data get API
 *
 * @param[in] switch_id SAI Switch object id
 * @param[in] obj_list SAI Switch object list
 * @param[in] clear_on_read Flag to clear the read data
 * @param[inout] buffer_size Actual buffer size in bytes
 * @param[out] buffer Data buffer
 *
 * @return #SAI_STATUS_SUCCESS on success, failure status code on error
 */
sai_status_t sai_tam_telemetry_get_data(
        _In_ sai_object_id_t switch_id,
        _In_ sai_object_list_t obj_list,
        _In_ bool clear_on_read,
        _Inout_ sai_size_t *buffer_size,
        _Out_ void *buffer);
```

#### 数据订阅粒度
> SAI driver will provide data at a coarse granularity and NOS will be responsible for discarding data or keeping a local cache. 
> This is in fact a better choice as NOS can keep a local copy for low frequency updated data.

#### TAM对象和绑定点
SAI提供的API均是按TAM各层次对象粒度的，各层次间对象关系见3.2节：   
![TAM_Obj](../../images/tam_obj.jpg)   

数据由switch中的data source生成；TAM对象需绑定到数据源上。
两种绑定方式：
- 源绑定(Source binding)：源的属性中指定TAM对象；
- 对象绑定(Object binding)：TAM对象自身包含源列表；  

首选方式1的提示机制。

#### 数据模型及序列化/反序列化(Serialization/De-serialization)
##### GPB(Google Protocol Buffer)
- [ProtoBuf开源地址](https://github.com/protocolbuffers/protobuf/releases)
- [ProtoBuf开发指南](https://developers.google.com/protocol-buffers/docs/proto)

GPB文件，.proto后缀的文件。  

## 配置
#### 如何新增数据属性

#### 如何新增Event

#### INT(Inband Network Telemetry)配置
INT是逐包逐流的数据收集。基于包的数据收集有两种构造形式：
- 插入metadata识别报文；
- 插入metadata和metadata头；

设备主要执行三种操作
- 初始化：创建监测报文的flow group。
- 发送：基于IFA/IOAM/Extn配置识别报文，给识别出的报文插入metadata；
- 终结：终结带metadata的报文。


# Data Plane Telemetry (DTEL)
[源文档](https://github.com/opencomputeproject/SAI/blob/master/doc/DTEL/SAI-Proposal-Data-Plane-Telemetry.md)

