
# 数据结构

- [树](trees.md)
- [堆](heap.md)
- [图](graph.md)

# 算法
## 算法性能(大O表示法)
#### 常见的算法性能
![perf](../images/algo_perf.png)
（汇总图综合文献1和2，注意文献2中的竖坐标有压缩）

- 常数时间 O(1)
- 对数时间 O(logn)
- 线性时间 O(n)

解释见文献1；
#### 大O的意义
数学上使用希腊字母表示函数式关系，大O表示函数式上边界；  
即，大O表示法描述算法性能时，O(x)表示算法的最差性能是x；

希腊字母意义，详见文献2
- Big O (O()) describes the upper bound of the complexity.
- Omega (Ω()) describes the lower bound of the complexity.
- Theta (Θ()) describes the exact bound of the complexity.
- Little O (o()) describes the upper bound excluding the exact bound.

## 基础算法

#### 递归(recursive)
每个递归函数都有两部分：[参考文档3；有的算法书无此概念]
- 基线条件(base case)，函数不再调用自己的终结条件
- 递归条件(recursive case)，函数调用自己的条件

``` c++
void countdown(int i)
    cout<<i;
  if (i <= 1)  // 基线条件
    return ; 
  else         // 递归条件
    countdown(i-1);
```

#### 分治算法(divide and conquer, D&C)
[参考文档3、4]
分治算法解决问题的步骤：
1. 找出基线条件，条件须尽可能简单；
2. 不断将问题分解(缩小规模)，直到符合基线条件。


快速排序、归并排序既是使用分治思想的算法。

#### 贪婪算法

#### 动态规划

#### 回溯法

## [排序(sort)算法](sort.md)

## 查找(或叫搜索)(search)算法
#### 二分查找

#### 深度优先搜索

#### 广度优先搜索

## 参考网站
1. [图解大 O 表示法](https://chinese.freecodecamp.org/news/big-o-notation/)
2. [What is Big O Notation Explained: Space and Time Complexity](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/)
3. 算法图解(像小说一样有趣的算法入门书)，Aditya Bhargava(著)，袁国忠(译)，2017
4. 数据结构、算法与应用(C++语言描述)(第2版)，Sartaj Sahni(著)，王立柱/刘志红(译)，2014
5. [算法可视](https://algorithm-visualizer.org)
6. [可视化算法](https://visualgo.net/en)
7. [C++ Data Structures and Algorithms Cheat Sheet](https://github.com/gibsjose/cpp-cheat-sheet/blob/master/Data%20Structures%20and%20Algorithms.md)


# 常见面试题
1. 查找性能的比较？ 
   - 简单查找：线性时间；
   - 二分查找：对数时间；
   - 散列表：常量时间；
2. xx
