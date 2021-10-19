
## 选择排序(Selection Sort)
*歌单排序：将歌单中的歌曲按照播放次数最多的排序，遍历歌单，找出播放次数最多的歌，添加到新列表中。*  

思路上最直接的排序算法。数组实现的步骤(使用临时空间存储已排序元素)：
1. 遍历未排序数组；
2. 每次遍历从未排序的数组中找出最大(小)值，追加到已排序数组中。

示例 (未使用额外空间，直接交换元素)
``` C++

template<typename T>
void selection_sort(std::vector<T>& arr) {
    for (int i = 0; i < arr.size() - 1; i++) {
        int min = i;
        for (int j = i + 1; j < arr.size(); j++)
            if (arr[j] < arr[min])
                min = j;
        std::swap(arr[i], arr[min]);
    }
}

```


## 冒泡排序(Bubble Sort)

示例
``` C++

template<typename T>
void bubble_sort(T arr[], int len) {
    int i, j;
    for (i = 0; i < len - 1; i++)
        for (j = 0; j < len - 1 - i; j++)
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
}
```

## 插入排序
*扑克插牌：*

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
2. [十大经典排序算法](https://www.runoob.com/w3cnote/ten-sorting-algorithm.html)
