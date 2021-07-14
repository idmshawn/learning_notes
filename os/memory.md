# 内存映射

### Linux内存地址空间
底部为0地址，往上为地址增长方向[参考文档1]

![image](https://user-images.githubusercontent.com/61963619/125583008-79cb1dcb-b400-44e9-93f7-71d98f38f6b5.png)


### 页号

linux提供以下预定义宏，用以获取页大小及页号。[参考文档2]

|宏名|说明|备注|
|--|--|--|
|PAGE_SHIFT|页偏移|通过对地址右移PAGE_SHIFT得到一个地址所在页的页号|
|PAGE_SIZE|内存页大小|不同平台上大小不同，范围可以从4KB到64KB|
|PAGE_MASK|页号掩码|地址与上PAGE_MASK，结果为这个地址所在的页面的页面号|

### 虚拟内存管理(VMM: Virtual Machine Manager)

vm_area_struct为VM area管理的结构体；（Linux 会把进程虚拟内存空间划分为多个分区，在 Linux 内核中使用 vm_area_struct 对象来表示）

remap_pfn_range: 将内核空间的内存映射到用户空间 [参考文档3~4]

mmap: 物理地址映射出虚拟地址


### 参考
1. [内存映射函数remap_pfn_range学习——示例分析（1）](https://www.cnblogs.com/pengdonglin137/p/8149859.html)
2. [LINUX内核中计算页面号](https://blog.csdn.net/chdhust/article/details/8889368)
3. [vm_area_struct （VMA）](http://abcdxyzk.github.io/blog/2015/09/09/kernel-mm-vm_area/)
4. [一文读懂 Linux 内存分配全过程](https://jishuin.proginn.com/p/763bfbd5733b)
