# Epoll

### 操作函数
见文献1 “epoll的工作原理”
- `int epoll_create(int size)` 创建一个epoll实例，该实例存在于系统内核空间；epoll实例会初始化一个列表，用于存储用户程序感兴趣的文件描述符，下文简称interest list；
- `int epoll_ctl(int epfd, int op, int fd, struct epoll_event *ev)` 对interest list增删改
- `int epoll_wait(int epfd, struct epoll_event *evlist, int maxevents, int timeout);` 调用该方法获取ready的文件描述符

### Epoll工作原理图示
1.进程483通过epoll_create()创建一个epoll实例，该实例存在于内核空间。

2.进程483通过epoll_ctl()系统调用，添加五个感兴趣的文件描述符到interest list。

3.当有文件描述符ready时，系统内核会把该文件描述符添加到ready list，ready list是interest list的子集。
事件发生后添加到ready list，这个过程是内核完成的。

4. 用户程序调用epoll_wait()时，内核会把ready list返回给用户程序。

# EventFd

### 操作函数
- `int eventfd(unsigned int initval, int flags);`创建一个eventfd文件描述符
- `int eventfd_read(int fd, eventfd_t *value);` 向eventfd中写入一个值
- `int eventfd_write(int fd, eventfd_t value);` 从eventfd中读出一个值

# 示例

eventfd可以被epoll监控， 一旦有状态变化，可以触发通知 (详见文献2)

```c
int g_iEvtfd = -1;

void *eventfd_child_Task(void *pArg)
{
    uint64_t uiWrite = 1;

    while(1)
    {
        sleep(2);
        if (0 != eventfd_write(g_iEvtfd, uiWrite))
        {
            printf("child write iEvtfd failed\n");
        }
    }

    return;
}

int main(int argc, char**argv[])
{
    int iEvtfd, j;
    uint64_t uiWrite = 1;
    uint64_t uiRead;
    ssize_t s;
    int iEpfd;
    struct epoll_event stEvent;
    int iRet = 0;
    struct epoll_event stEpEvent;
    pthread_t stWthread;

    iEpfd = epoll_create(1);
    if (-1 == iEpfd)
    {
        printf("Create epoll failed.\n");
        return 0;
    }

    iEvtfd = eventfd(0,0);
    if (-1 == iEvtfd)
    {
        printf("failed to create eventfd\n");
        return 0;
    }

    g_iEvtfd = iEvtfd;

    memset(&stEvent, 0, sizeof(struct epoll_event));
    stEvent.events = (unsigned long) EPOLLIN;
    stEvent.data.fd = iEvtfd;
    iRet = epoll_ctl(iEpfd, EPOLL_CTL_ADD, g_iEvtfd, &stEvent);
    if (0 != iRet)
    {
        printf("failed to add iEvtfd to epoll\n");
        close(g_iEvtfd);
        close(iEpfd);
        return 0;
    }

    iRet = pthread_create(&stWthread, NULL, eventfd_child_Task, NULL);
    if (0 != iRet)
    {
        close(g_iEvtfd);
        close(iEpfd);
        return;
    }

    for(;;)
    {
        iRet = epoll_wait(iEpfd, &stEpEvent, 1, -1);
        if (iRet > 0)
        {
            s = eventfd_read(iEvtfd, &uiRead);
            if (s != 0)
            {
                printf("read iEvtfd failed\n");
                break;
            }
            printf("Read %llu (0x%llx) from iEvtfd\n", uiRead, uiRead);
        }
    }

    close(g_iEvtfd);
    close(iEpfd);
    return 0;
}

```


## 参考
1. [关于非阻塞I/O、多路复用、epoll的杂谈](https://bbs.huaweicloud.com/blogs/137781)
2. [线程间通信之eventfd](https://www.cnblogs.com/zhengchunhao/p/5335914.html)

