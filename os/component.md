
## Wait Queue
#### 简介
Linux内核中，当等待某件事件发生时可以使当前进程以休眠的方式进行等待，这样不会占用cpu资源，当事件发生的时候则将其唤醒；
等待队列（wait queue）用于使线程等待某一特定的事件发生而无需频繁的轮询，进程在等待期间睡眠，在某件事发生时由内核自动唤醒。
它是以双循环链表为基础数据结构，与进程的休眠唤醒机制紧密相联，是实现异步事件通知、跨进程通信、同步资源访问等技术的底层技术支撑。

#### 基本操作

wait_event_interruptible()等待函数，使用sleep进入休眠，`__wait_event`等待条件成立时唤醒。
init_waitqueue_head()初始化等待队列头，初始化的对象wait_queue_head_t是等待队列的基础结构；

	struct __wait_queue_head {
	    spinlock_t        lock;  //用于互斥访问的自旋锁
	    struct list_head    task_list;
	};
	typedef struct __wait_queue_head wait_queue_head_t;


#### 参考文档
1. [内核中的等待队列](https://zhuanlan.zhihu.com/p/60713292)
2. [Linux内核之休眠与唤醒](https://sourcelink.top/2020/07/15/linux-wake-up/)


## Atomic

原子操作是指**某一操作在执行过程中是不可以被打断的，它要么全部执行完毕，要么就一点也不执行**。也就是说原子操作是绝对不会出现该操作执行了一半，内核又去执行其他操作的情况。

linux专门定义了一种只进行原子操作的类型atomic_t，并提供相关的原子读写调用API。各个CPU平台有各自的原子操作实现方式，基本都是通过汇编实现的。
atomic_t其实是int类型，只是禁止寄存器对其暂存：

	typedef struct {
	    volatile int counter;
	} atomic_t;

原子操作主要用于实现资源计数。操作函数
- atomic_set：设置计数变量置
- atomic_read：读取计数变量值
- atomic_inc/atomic_dec：计数递增/递减
- atomic_add/atomic_sub

#### 参考文档
1. [原子性操作atomic_t](https://blog.csdn.net/a775992553/article/details/8797474?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-8.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-8.control)
