# 内存映射

### 页号

linux提供以下预定义宏，用以获取页大小及页号。

|宏名|说明|备注|
|--|--|--|
|PAGE_SHIFT|页偏移|通过对地址右移PAGE_SHIFT得到一个地址所在页的页号|
|PAGE_SIZE|内存页大小|不同平台上大小不同，范围可以从4KB到64KB|
|PAGE_MASK|页号掩码|地址与上PAGE_MASK，结果为这个地址所在的页面的页面号|

### 虚拟地址空间映射

remap_pfn_range: 将内核空间的内存映射到用户空间

mmap: 物理地址映射出虚拟地址


### 参考
1. [LINUX内核中计算页面号](https://blog.csdn.net/chdhust/article/details/8889368)
2. [内存映射函数remap_pfn_range学习——示例分析（1）](https://www.cnblogs.com/pengdonglin137/p/8149859.html)
3. [struct vm_area_struct结构体学习](https://blog.csdn.net/SweeNeil/article/details/83902755)
