# 内存映射

### Linux内存地址空间
底部为0地址，往上为地址增长方向[参考文档1]

![image](https://user-images.githubusercontent.com/61963619/125583008-79cb1dcb-b400-44e9-93f7-71d98f38f6b5.png)

1. bss(Block Started by Symbol) 
bss是指那些没有初始化的和初始化为0的全局变量和静态变量,bss类型的全局变量只占运行时的内存空间，而不占文件空间。 
另外，大多数操作系统，在加载程序时，会把所有的bss全局变量全部清零，无需要你手工去清零。 
但为保证程序的可移植性，手工把这些变量初始化为0也是一个好习惯。 
2. data 
与bss相比，data就容易明白多了，它的名字就暗示着里面存放着数据。当然，如果数据全是零，为了优化考虑，编译器把它当作bss处理。通俗的说，data指那些初始化过（非零）的非const的全局变量和静态变量。 
由此可见，data类型的全局变量是即占文件空间，又占用运行时内存空间的。 
3. rodata 
rodata的意义同样明显，ro代表read only，即只读数据(const)。只读数据段，存放常量，字符常量，const常量，据说还存放调试信息。关于rodata类型的数据，要注意以下几点： 
常量不一定就放在rodata里，有的立即数直接编码在指令里，存放在代码段(.text)中。 
对于字符串常量，编译器会自动去掉重复的字符串，保证一个字符串在一个可执行文件(EXE/SO)中只存在一份拷贝。 
rodata是在多个进程间是共享的，这可以提高空间利用率。 
在有的嵌入式系统中，rodata放在ROM(如norflash)里，运行时直接读取ROM内存，无需要加载到RAM内存中。 
在嵌入式linux系统中，通过一种叫作XIP（就地执行）的技术，也可以直接读取，而无需要加载到RAM内存中。 
由此可见，把在运行过程中不会改变的数据设为rodata类型的，是有很多好处的：在多个进程间共享，可以大大提高空间利用率，甚至不占用RAM空间。同时由于rodata在只读的内存页面(page)中，是受保护的，任何试图对它的修改都会被及时发现，这可以帮助提高程序的稳定性。 
4. text 
通常是指用来存放程序执行代码的一块内存区域。这部分区域的大小在程序运行前就已经确定，并且内存区域通常属于只读, 某些架构也允许代码段为可写，即允许修改程序。在代码段中，也有可能包含一些只读的常数变量，例如字符串常量等。 

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
