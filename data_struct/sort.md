
## 选择排序(Selection Sort)


## 冒泡排序(Bubble Sort)


## 快速排序(Quicksort)


## 应用
C/C++中虽然有qsort库函数，但[其实现并不一定使用的是快排](https://en.cppreference.com/w/cpp/algorithm/qsort)：
> Despite the name, C++, C, and POSIX standards do not require this function to be implemented using quicksort or make any complexity or stability guarantees.

各排序算法的比较参考文档1的“4.0 Algorithms”， 算法性能比较汇总如下

|算法|空间复杂度|时间复杂度(平均)|最好时间|最差时间|
|--|--|--|--|--|
|选择排序|O(1)|O(n^2)|Already sorted, O(n^2)|Reverse sorted, O(n^2)|
|冒泡排序|O(1)|O(n^2)|Already sorted, O(n)|Reverse sorted, O(n^2)|
|快速排序|O(n)|O(nlog(n))|O(nlog(n))|All elements equal, O(n^2)|


## 参考文档
1. [C++ Data Structures and Algorithms Cheat Sheet](https://github.com/gibsjose/cpp-cheat-sheet/blob/master/Data%20Structures%20and%20Algorithms.md)
