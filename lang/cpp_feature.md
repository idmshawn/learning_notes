c++核心知识及C++11新特性总结
## C++基础
### 引用
引用即别名，和指针的区别：
1. 引用的声明周期一直与原值(被引用值)绑定，不能切换到其它值；
2. 引用必须定义时赋初值，而指针不用；
相同：
改引用的值，被引用值也变更；
改指针的内容，原指针指向的内容也变更；

### 函数
函数参数传递
形参：函数定义和声明时的形式参数；实参，函数被实际调用时传入的参数；

|参数类型|原理|差异1|差异2|
|--|--|--|--|
|传值参数|函数实参被**拷贝**给形参|拷贝对象大时性能低|由于是拷贝，函数对形参做的所有操作不会影响到实参|
|传址调用(指针形参)|指针拷贝，之后有两个不同的指针，指向同一位置|||
|传引用参数|形参**绑定**到对应的实参上|无拷贝操作|函数操作形参后，对应的实参也发生变更|

**C语言常使用指针类型的形参访问函数外部的对象，C++中建议使用引用类型的形参代替指针**。

### 类
###### 类成员

###### 构造函数
* 构造函数没有返回类型；
* 类可以包含多个构造函数，一般用作参数重载；
* 构造函数不能声明成const的；

###### 析构函数
* 析构

### 模板
###### 函数模板
定义示例：
  `template <typename T>
  int compare(const T &v1, const T &v2)
  {
  }`

模板参数列表中可定义普通类型参数。

函数模板参数一般都是const的引用？？？

###### 类模板


### 容器
###### 顺序容器
根据元素加入容器的顺序访问元素；如vector、array、string、list。

顺序容器常用方法
|方法|说明|备注|
|--|--|--|
|c.begin()|起始元素||
|c.end()|最后元素||
|**c.push_back()**|在容器尾部追加元素||
|c.push_front()|在容器首部追加元素||
|c.pop_back()|删除容器中尾元素||
|c.pop_front()|删除容器中首元素||
|c.insert(p,t)|在中间插入||
|c.insert(p,t)|在中间插入||
|c.back()|||
|c.front()|||
|c.erase(p)|删除容器中指定元素||
|c.\[n\]|按下标索引||

###### 关联容器
根据关键字的值存储元素；如map、pair、set。

关联容器常用方法
|方法|说明|备注|
|--|--|--|
|c.insert(v)|插入元素，类似操作还有emplace||
|c.insert(b, e)|||
|c.erase(k)|删除元素||
|c.erase(b, e)|删除迭代器b和e范围间的元素||
|c\[n\]|访问元素，map支持下标索引||
|c.find(k)|访问元素，查找元素||
|c.count(k)|访问元素，||
|c.low_bound(k)|访问元素，||
|c.upper_bound(k)|访问元素，||

###### 无序容器


###### 迭代器
[C++ iterator介绍](http://c.biancheng.net/view/338.html)

## C++11新特性

* auto：类型占位符，通知编译器去根据初始化代码推断所声明变量的真实类型；
* decltype：根据表达式返回值推断类型；
* using：模板别名；
* 基于范围的for循环
* constexpr：不仅可以修饰变量，还可以修饰表达式和函数返回值；
* noexcept：不抛出异常，noexcept几乎总是和constexpr一起使用
* std::array：新增的顺序容器，固定大小；
* type traits：简言之，[type traits](https://blog.csdn.net/mogoweb/article/details/79264925)是新提供一个`#include <type_traits>`头文件，“里面包含了几乎所有数据类型的类型特征，它可以告诉数据的基本类型、是否指针、是否数组等等”。
用户可以引用此头文件简化自己函数中的类型判断，以支持模板化的泛型编程。
* static_assert：编译时的断言检查。如果断言为假，编译器会打印一个特殊的错误信息。运行时什么也不会干。


## C++实现

### C++接口类(Interface)实现
设计模式书籍或很多类图中，会有类标以<<Interface>>，为面向对象语言中的接口类。  
Java直接使用interface和abstract关键字定义接口类和抽象类，C++没有这种关键字。    
C++使用抽象类实现接口。

## 参考
1. C++手册：[cppreference](https://en.cppreference.com/w/)
2. [泛型编程与STL](https://blog.csdn.net/zl6481033/article/details/89465421?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control&dist_request_id=1328665.10354.16159908009496807&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control)
3. [C++那些事](https://light-city.club/sc/)

### 面试参考
* 指针与引用的区别？ 传值参数和传引用参数的差异点？
* 类和结构体的区别？  类的成员默认是private，结构体的成员默认是public；
* C++如何实现多态？ 
* 重载(Overload)与重写(Override)的区别？ 重载：同名的函数，参数等不同；重写：同样的函数重新定义；
