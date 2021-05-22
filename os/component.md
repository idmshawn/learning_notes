
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

其它函数
atomic_set
atomic_inc
atomic_read


#### 参考文档
1. [内核中的等待队列](https://zhuanlan.zhihu.com/p/60713292)
2. [Linux内核之休眠与唤醒](https://sourcelink.top/2020/07/15/linux-wake-up/)
