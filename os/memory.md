# 内存映射

### 页操作

|宏名|说明|备注|
|--|--|--|
|PAGE_SHIFT|页偏移|通过对地址右移PAGE_SHIFT得到一个地址所在页的页号|
|PAGE_SIZE|内存页大小|不同平台上大小不同，范围可以从4KB到64KB|
|PAGE_MASK|页号掩码|地址与上PAGE_MASK，结果为这个地址所在的页面的页面号|


### 参考
1. [LINUX内核中计算页面号](https://blog.csdn.net/chdhust/article/details/8889368)
