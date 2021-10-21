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

## 选择排序(Selection Sort)
*歌单排序：将歌单中的歌曲按照播放次数最多的排序，遍历歌单，找出播放次数最多的歌，添加到新列表中。*  [参考文档3]

思路上最直接的排序算法。实现步骤(数组实现，使用临时空间存储已排序元素)：
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

## 插入排序(Insertion Sort)
*扑克插牌：*

## 快速排序(Quick Sort)
*思路主要记quick_sort部分，即以下实现步骤；分隔函数不做主要记忆*
#### 实现步骤(数组实现)
1. 从待排序数组中选一个元素作为“基准值”(pivot)；
2. 分区：重新排序数列，所有比基准值小的元素放在基准前面，所有比基准值大的元素放在基准的后面（相同的数可以到任一边）；
3. 对基准前后的两个子数组递归排序，即回到步骤1；

#### 分割函数

#### 示例(递归实现，综合文档2及其它，C++改造)
``` C++
/* 严蔚敏《数据结构》标准分割函数；
实现两个功能：1、元素按大小移到pivot两侧；2、返回一个中间位置的pivot？
*/
template <typename T>
int partition(vector<T> &a, int low, int high)
{
    int pivot = a[low]; // 此处的pivot是元素值
    while (low < high) {
        while (low < high && a[high] > pivot) {
            high--;
	}
	a[low] = a[high];
	while (low < high && a[low] < pivot) {
	    low++;
	}
        a[high] = a[low];
    }

    a[low] = pivot;
    return low;
}

template <typename T>
void quick_sort(vector<T> &a, int low,int high)
{
    if (low < high) {  // low等于大于high时，递归条件终止
        int p = partition(a, low, high);  // 此处的p是元素位置，即数组下标索引; 未免混淆，不再用pivot变量名
	quick_sort(a, low, p - 1);
	quick_sort(a, p + 1, high);
    }
}
```
#### 应用
C/C++中虽然有qsort库函数，但[其实现并不一定使用的是快排](https://en.cppreference.com/w/cpp/algorithm/qsort)：
> Despite the name, C++, C, and POSIX standards do not require this function to be implemented using quicksort or make any complexity or stability guarantees.

## 归并排序(Merge Sort)

示例(递归实现，综合文档2及其它，C++改造)
``` C++
template <typename T>
void merge(vector<T> &a, int front, int mid, int end) {
    vector<T> LeftSubArray(a.begin() + front, a.begin() + mid + 1);
    vector<T> RightSubArray(a.begin() + mid + 1, a.begin() + end + 1);
    int idxLeft = 0, idxRight = 0;
 
    LeftSubArray.insert(LeftSubArray.end(), numeric_limits<int>::max());
    RightSubArray.insert(RightSubArray.end(), numeric_limits<int>::max());

    for (int i = front; i <= end; i++) {
        if (LeftSubArray[idxLeft] < RightSubArray[idxRight]) {
            a[i] = LeftSubArray[idxLeft];
            idxLeft++;
        } else {
            a[i] = RightSubArray[idxRight];
            idxRight++;
        }
    }
}

template <typename T>
void merge_sort(vector<T> &a, int front, int end) {
  if (front >= end) return;
  int mid = front + (end - front) / 2;
  merge_sort(a, front, mid);
  merge_sort(a, mid + 1, end);
  merge(a, front, mid, end);
}
```

## 算法比较
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
4. [OI Wiki:排序](https://oi-wiki.org/basic/sort-intro/)
