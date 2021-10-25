# 图搜索

## 广度优先搜索(Breadth First Search, BFS)
*在朋友关系的图中找芒果销售商；你的朋友中没有销售商时，将朋友的朋友加入搜索名单。*  
BFS可用于解决非加权有向图中的**最短路径问题**(shortest-path problem)。

BFS回答两类问题：
1. 从节点A出发，有前往B的路径吗？(*你的人际关系网中，有芒果销售商吗？*)
2. 从节点A出发，前往节点B的哪条路径最短？(*哪个芒果销售商与你的关系最近？*)

为解决2类问题，需保证一度关系朋友、二度关系朋友等按先后顺序加入搜索名单，使用**FIFO队列**数据结构保证顺序。

#### 实现步骤
BFS针对示例问题的实现
1. 创建一个队列，用于存储要检查的人；
2. 从队列中弹出一个人；
3. 检查这个人是否是芒果销售商；
4. 检查结果：  
  a. 是，则算法结束；  
  b. 否，则将此人的所有邻居节点都加入队列；返回第2步；
5. 如果队列为空，说明人际关系网中没有芒果销售商。算法结束。

注：检查完一人后，应标记为已检查，且不再检查他，否则可能导致无限循环。

#### 性能
BFS性能为O(*V*+*E*)，其中V为顶点(vertice)，E为边数(Edge)

#### 示例

## 深度优先搜索(Depth First Search, DFS)


## Dijkstra算法
BFS用于在非加权图中查找最短路径；Dijkstra算法用于在加权图中查找最短路径。  
Dijkstra算法由荷兰计算机科学家 E. W. Dijkstra 于1956年发现，1959年公开发表。是一种求解**非负权图**上**单源最短路径**(SSSP：Single-Source Shortest Path)的算法。  
核心思想：(同贪婪算法)每步都找到局部最优解。

#### 应用场景
[参考文档1]：  
Dijkstra只适用于有向无换图(directed acyclic gragh, DAG)；  
仅当权重为正时Dijkstra算法才管用，若图中包含负权边，请使用贝尔曼-福德算法；

#### 实现步骤
1. **找出“最便宜”的节点**，即可在最短时间内到达的节点；
2. 对于该节点的邻居，检查是否有前往它们的更短路径；如果有，就更新到邻居节点的开销；
3. 重复此过程，直到对图中的每个节点都这样操作了；
4. y计算最终路径  
[具体实现参考文档2的步骤与图解]  

## Bellman-Ford算法
Bellman-Ford 算法和 Dijkstra 算法同为解决单源最短路径的算法。  
> Dijkstra 算法采用[贪心算法](base_algo.md#贪婪算法)范式进行设计，普通实现的时间复杂度为 O(V2)，若基于 Fibonacci heap 的最小优先队列实现版本则时间复杂度为 O(E + VlogV)。
> Bellman-Ford 算法采用[动态规划](base_algo.md#动态规划)进行设计，实现的时间复杂度为 O(V*E)，其中 V 为顶点数量，E 为边的数量。  

## 参考
1. 算法图解
2. [Dijkstra 单源最短路径算法](https://www.cnblogs.com/gaochundong/p/dijkstra_algorithm.html)  
3. [Bellman-Ford 单源最短路径算法](https://www.cnblogs.com/gaochundong/p/bellman_ford_algorithm.html)
4. [最短路](https://oi-wiki.org/graph/shortest-path/)
