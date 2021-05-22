# Linux内核组件

## 内核模块基础

#### 内核模块定义
ko入口函数一般用__init定义，出口函数用__exit定义，且会通过module_init和module_exit注册；

内核模块的预定义宏：
- MODULE_AUTHOR 内核作者
- MODULE_DESCRIPTION 内核模块描述
- MODULE_LICENSE 内核证书类型

一个内核module的定义示例：

	static int32 __init my_module_init(void) 
	{ 
	}
	
	static void __exit my_module_exit(void) 
	{ 
	}
	
	module_init(my_module_init);
	module_exit(my_module_exit);

	MODULE_DESCRIPTION("A sample of linux kernel module");
	MODULE_AUTHOR("Shawn");
	MODULE_LICENSE("GPL");


#### 内核加载/卸载
- 加载ko 
`insmod my_module.ko `
- 卸载ko
`rmmod my_module`
- 查看加载的内核module
`lsmod`

#### 内核日志
printk()用于记录日志，以下宏指定日志级别(定义在include/linux/kernel.h中)，KERN_EMERG最高，KERN_DEBUG最低

	#define KERN_EMERG "<0>" /* system is unusable */
	#define KERN_ALERT "<1>" /* action must be taken immediately */
	#define KERN_CRIT "<2>" /* critical conditions */
	#define KERN_ERR "<3>" /* error conditions */
	#define KERN_WARNING "<4>" /* warning conditions */
	#define KERN_NOTICE "<5>" /* normal but significant condition */
	#define KERN_INFO "<6>" /* informational */
	#define KERN_DEBUG "<7>" /* debug-level messages */

`dmesg`命令用于打印内核记录的日志。

#### 模块参数指定
module_param用来定义对外参数，这些参数可以在插入ko时指定；
MODULE_PARM_DESC用来描述参数信息或使用方法；示例：

	int my_param = 0;
	module_param(my_param, int, 0);  /* 定义int类型的参数my_param，默认值为0 */
	MODULE_PARM_DESC(my_param, "You can specific my_param with value 0~3 (default 0).");

ko插入时指定参数插入

	insmod my_module.ko my_param=3

#### 参考文档
1. [Linux Kernel Modules](https://cs4118.github.io/dev-guides/linux-modules.html)


## 字符设备注册
允许使用设备名称创建一个内核设备对象，如创建一个`my_obj`的设备对象，在linux下即可查到`/dev/my_obj`。

支持静态注册(指定设备编号来注册)和动态分配(不指定设备编号来注册)。静态分配时需要指定设备编号。

常用函数及功能(详见参考文档1)

|函数|功能|备注|
|--|--|--|
|register_chrdev_region|指定设备编号来静态注册一个字符设备||
|alloc_chrdev_region|动态分配一个字符设备,注册成功并将分配到的主次设备号放入dev里||
|cdev_init|初始化cdev结构体,并将file_operations结构体放入cdev-> ops 里||
|cdev_add|将cdev结构体添加到系统中||

#### 参考文档
1. [使用register_chrdev_region系列来注册字符设备](https://www.cnblogs.com/lifexy/p/7827559.html)


## 地址操作


常用函数及功能

|函数|功能|备注|
|--|--|--|
|virt_to_page|||
|SetPageReserved|||
|pci_register_driver|||



## Wait Queue
#### 简介
Linux内核中，当等待某件事件发生时可以使当前进程以休眠的方式进行等待，这样不会占用cpu资源，当事件发生的时候则将其唤醒；
等待队列（wait queue）作为一种异步事件通知机制，可用来实现阻塞进程的唤醒。

#### 常用函数及功能

|函数|功能|备注|
|--|--|--|
|wait_event_interruptible|使用sleep进入休眠，`__wait_event`等待某个条件成立时唤醒||
|init_waitqueue_head|||
|atomic_set|||
|atomic_inc|||
|atomic_read|||


#### 参考文档
1. [Linux内核之休眠与唤醒](https://sourcelink.top/2020/07/15/linux-wake-up/)
2. [浅析Linux等待队列](https://www.cnblogs.com/noaming1900/archive/2011/01/14/1935528.html)

