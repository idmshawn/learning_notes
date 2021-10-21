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

## 插入排序(Insertion Sort)
*扑克插牌：*


## 选择排序(Selection Sort)
*歌单排序：将歌单中的歌曲按照播放次数最多的排序，遍历歌单，找出播放次数最多的歌，添加到新列表中。*  [参考文档3]

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

## 归并排序(Merge Sort)

示例(递归实现)
``` C++
void Merge(vector<int> &Array, int front, int mid, int end) {
    vector<int> LeftSubArray(Array.begin() + front, Array.begin() + mid + 1);
    vector<int> RightSubArray(Array.begin() + mid + 1, Array.begin() + end + 1);
    int idxLeft = 0, idxRight = 0;
    LeftSubArray.insert(LeftSubArray.end(), numeric_limits<int>::max());
    RightSubArray.insert(RightSubArray.end(), numeric_limits<int>::max());

    for (int i = front; i <= end; i++) {
        if (LeftSubArray[idxLeft] < RightSubArray[idxRight]) {
            Array[i] = LeftSubArray[idxLeft];
            idxLeft++;
        } else {
            Array[i] = RightSubArray[idxRight];
            idxRight++;
        }
    }
}

void MergeSort(vector<int> &Array, int front, int end) {
    if (front >= end)
        return;
    int mid = (front + end) / 2;
    MergeSort(Array, front, mid);
    MergeSort(Array, mid + 1, end);
    Merge(Array, front, mid, end);
}

```

## 快速排序(Quick Sort)
数组实现的步骤：
1. 从待排序数组中选一个元素作为“基准值”(pivot)；
2. 分区：重新排序数列，所有比基准值小的元素放在基准前面，所有比基准值大的元素放在基准的后面（相同的数可以到任一边）；
3. 对基准前后的两个子数组递归排序，即回到步骤1；

示例(递归实现)
``` C++
template <typename T>
void quick_sort_recursive(T arr[], int start, int end) {
    if (start >= end)
        return;
    T mid = arr[end];
    int left = start, right = end - 1;
    while (left < right) { //在整个范围内搜寻比枢纽元值小或大的元素，然后将左侧元素与右侧元素交换
        while (arr[left] < mid && left < right) //试图在左侧找到一个比枢纽元更大的元素
            left++;
        while (arr[right] >= mid && left < right) //试图在右侧找到一个比枢纽元更小的元素
            right--;
        std::swap(arr[left], arr[right]); //交换元素
    }
    if (arr[left] >= arr[end])
        std::swap(arr[left], arr[end]);
    else
        left++;
    quick_sort_recursive(arr, start, left - 1);
    quick_sort_recursive(arr, left + 1, end);
}

template <typename T>
void quick_sort(T arr[], int len) {
    quick_sort_recursive(arr, 0, len - 1);
}

```

## 应用
C/C++中虽然有qsort库函数，但[其实现并不一定使用的是快排](https://en.cppreference.com/w/cpp/algorithm/qsort)：
> Despite the name, C++, C, and POSIX standards do not require this function to be implemented using quicksort or make any complexity or stability guarantees.

各排序算法的比较参考文档1的“4.0 Algorithms”， 算法性能比较汇总如下

|算法|空间复杂度|时间复杂度(平均)|最好时间|最差时间|
|--|--|--|--|--|
|冒泡排序|O(1)|O(n^2)|Already sorted, O(n)|Reverse sorted, O(n^2)|
|插入排序|O(1)|O(n^2)|Already sorted, O(n)|Reverse sorted, O(n^2)|
|选择排序|O(1)|O(n^2)|Already sorted, O(n^2)|Reverse sorted, O(n^2)|
|归并排序|O(n)|O(nlog(n))|O(nlog(n))|Reverse sorted, O(nlog(n))|
|快速排序|O(n)|O(nlog(n))|O(nlog(n))|All elements equal, O(n^2)|

## 参考文档
1. [C++ Data Structures and Algorithms Cheat Sheet](https://github.com/gibsjose/cpp-cheat-sheet/blob/master/Data%20Structures%20and%20Algorithms.md)
2. [十大经典排序算法](https://www.runoob.com/w3cnote/ten-sorting-algorithm.html)
3. 算法图解(像小说一样有趣的算法入门书)，Aditya Bhargava(著)，袁国忠(译)，2017
