# 基础数据结构

## 数组和链表

## 散列表

## 队列和栈
队列：FIFO(First In First Out)
栈：LIFO(Last In First Out)

#### 单调栈
单调栈实际上就是栈，只是限制要比普通的栈更严格而已了[文档4]：  
要求是每次入栈的元素必须要有序（如果新元素入栈不符合要求，则将之前的元素出栈，直到符合要求再入栈），使之形成单调递增/单调递减的一个栈。  
单调递增/递减栈是根据出栈后的顺序来决定的。**单调递增栈**：只有比栈顶小的才能入栈，否则就把栈顶出栈后，再入栈。  
例题: [LeetCode:每日温度](https://leetcode.cn/problems/daily-temperatures/solution/mei-ri-wen-du-by-leetcode-solution/)  

## 字典(dictionary)
字典是由一些形如(*k*,*v*)的数对所组成的集合，其中*k*是**关键字**，*v*是与关键字*k*对应的**值**。任意两个数对，其关键字都不等。

- C++实现[文档2]：C++中的关联容器`map`、`set`、`unordered_map`、`unordered_set`(unordered为hash实现的映射)等实现的就是字典。  
- Python实现[文档3]：Python中的唯一映射类型便是字典；从python2.2起，可用库函数`dict()`创建字典。

## 优先级队列(priority queue)
与普通FIFO队列不同，优先级队列中，元素出队列的顺序由元素的优先级决定。**[堆](heap.md)(heap)是实现优先级队列效率很高的数据结构**。

- C++实现：STL类priority-queue是用堆实现了优先级队列。

## [树](trees.md)

## [图](graph.md)

## 其它
#### 跳表
为提高有序链表的查找性能，可在全部或部分节点上增加额外的指针；查找时，通过这些指针跳过链表的若干节点，不必从左到右连续查看所有的节点。增加了额外的向前指针的链表叫做跳表(skip list)。[文档1]


## 参考文档
1. 数据结构、算法与应用(C++语言描述)
2. C++ Primer(第5版)
3. Python核心编程(第2版)
4. [单调栈技巧总结](https://www.cnblogs.com/liang24/p/14200734.html)
