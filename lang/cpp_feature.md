# C++基础
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

### 构造函数与析构函数

构造
- 构造函数没有返回类型；
- 类可以包含多个构造函数，一般用作参数重载；
- 构造函数不能声明成const的；  

析构
- 没有返回类型；
- 不接受参数；

构造函数有一个初始化部分和一个函数体；  
析构函数有一个函数体和一个析构部分；

#### 执行机制
执行时序[见C++ Primer p445]     
- 构造函数中，**成员的初始化是在函数体执行之前完成的**，且按照它们在类中出现的顺序初始化。
- 析构函数中，**首先执行函数体，然后销毁成员**。成员按照初始化顺序的逆序销毁。(即，析构函数体自身并不直接销毁成员，成员是在析构函数体之后隐含的析构阶段中被销毁的。)

什么时候调用析构函数[见C++ Primer p445]   
无论何时一个对象被销毁，就会自动调用其析构函数：  
- 变量在离开其作用域时被销毁；
- 当一个对象被销毁时，其成员被销毁；
- 容器被销毁时，其元素被销毁；
- 动态分配的对象，当对指向它的指针应用delete运算符时被销毁；
- 临时对象，当创建它的完整表达式结束时被销毁。

### 内存管理
- [new和delete](cpp_mem_mng.md)
- [智能指针](cpp_mem_mng.md#%E6%99%BA%E8%83%BD%E6%8C%87%E9%92%88)

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
map与unordered_map对比[文档11]：  
- 前者为红黑树实现，有序，操作时间O(lgn)，缺点是空间占用率高；
- 后者为hash实现，hash映射，查找时间O(1)，缺点建立耗费时间；

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


# C++11新特性

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

# C++实现

### 接口和抽象类
"我们可以使用接口来实现面向对象的抽象特性、多态特性和基于接口而非实现的设计原则；使用抽象类来实现面向对象的继承特性和模板设计模式等。"   
- **抽象类**更多的是为了代码**复用**；  
- **接口**就更侧重于**解耦**(抽象)。  

Java直接使用Interface和Abstract关键字定义接口类和抽象类，C++没有这种关键字，但可以间接实现这两个功能。  
#### 抽象类
OOP中的抽象类：
- 是一种**只能定义类型，而不能产生对象**(实例化)的类；  
- 只能**被继承，并重写**相关函数；(子类继承抽象类，必须实现抽象类中的所有抽象方法)  

C++通过纯虚函数(virtual + “=0”)实现抽象类
- 存在纯虚函数的类是抽象类(如下面的shape类)
- 如果子类没有实现所有的纯虚函数，则子类仍然是抽象类

``` mermaid
classDiagram
%% commit
class Shape
<<abstract>> Shape
Shape <|.. Rect : Realization
Shape <|.. Circle: Realization
Shape: +int id
Shape: +area()

class Rect{
  +int id
  -int a
  -int b
  +area()
}
class Circle{
  +int id
  -int r
  +area()
}
```

``` c++
class Shape {
public:
    int id;
    virtual double area() = 0;  // 抽象类定义纯虚函数
};

class Rect : public Shape {
public:
    int id;    
    double area() { // 子类重写纯虚函数
        // ...
    }
private:
    int a;
    int b;
};
```

#### 接口
C++使用抽象类实现接口。满足下面条件的C++类称为接口
- 类中没有定义任何变量；(接口**不能包含属性**，也就是成员变量)  
- 所有的成员函数都是纯虚函数，且是公有的；(接口**只能声明方法**，方法不能包含代码实现)
- 类实现接口的时候，必须实现接口中声明的所有方法。

``` mermaid
classDiagram
%% commit
class Channel
<<interface>> Channel
Channel: +open()
Channel: +close()
Channel: +send()
Channel: +receive()
```

``` c++
class Channel {
public:
    virtual bool open() = 0;
    virtual void close() = 0;
    virtual bool send(char* buf, int len) = 0;
    virtual int receive(char* buf, int len) = 0;
};
```

#### 如何决定该用抽象类还是接口？
- 如果一个类是父类，就要考虑它有没有必要成为一个抽象类，判断准则是这个父类有没有必要产生一个对象，没必要则做成抽象类。  
- “如果我们要表示一种is-a的关系，并且是为了解决代码复用的问题，我们就用抽象类；  
如果我们要表示一种has-a关系，并且是为了解决抽象而非代码复用的问题，那我们就可以使用接口。”  
- “从类的继承层次上来看，抽象类是一种自下而上的设计思路，先有子类的代码重复，然后再抽象成上层的父类（也就是抽象类）。  
而接口正好相反，它是一种自上而下的设计思路。我们在编程的时候，一般都是先设计接口，再去考虑具体的实现。”

### 异常处理
C++默认支持异常处理，C++异常处理包含(见C++ Primer)：
###### 1. throw表达式
异常检测使用；比如，使用throw表达式直接引发异常
```c++
if (xxx)
  throw runtime_error("Data must xxx");
```
###### 2. try-catch语句块
异常处理代码；
```c++
try {
  // 代码块正常执行，其中可能抛出异常
} catch (runtime_error err) {
  // 异常处理
}
```
栈展开的过程中，找不到任何匹配的catch时，则调用terminate终结程序。
###### 3. 一套异常类(exception class)
用于在throw表达式和相关的catch子句之间传递异常的具体信息；

标准库中定义了一些常用的异常类
|异常类|头文件|说明|
|--|--|--|
|exception|exception|最通用的异常类，只报告异常的发生，不提供任何额外信息|
|runtime_error|stdexcept|只有在运行时才能检测出的问题|
|logic_error|stdexcept|无效参数等其它逻辑错误|
|bad_alloc|new|new不能分配要求的内存空间时，抛出此异常；可使用placement new禁止异常(见C++ primer p408、p729)|
|bad_cast|type_info||

#### noexcept
C++ 11之后支持noexcept，noexcept操作符的作用是阻止异常的传播。  
C++中的异常处理是在运行时而不是编译时检测的。为了实现运行时检测，编译器创建额外的代码。  
noexcept告诉编译器，函数中不会发生异常,这有利于编译器对程序做更多的优化。  
在新版本的编译器中，析构函数是默认加上关键字noexcept的。

如果在运行时，noexecpt函数向外抛出了异常（如果函数内部捕捉了异常并完成处理，这种情况不算抛出异常），程序会**直接终止，调用std::terminate()函数，该函数内部会调用std::abort()终止程序**。

## 参考
1. C++手册：[cppreference](https://en.cppreference.com/w/)
2. [C++那些事](https://light-city.club/sc/)
3. [C++ STL与泛型编程（三）](https://blog.csdn.net/zl6481033/article/details/89465421?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control&dist_request_id=1328665.10354.16159908009496807&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control)
4. [泛型编程、STL的概念、STL模板思想及其六大组件的关系，以及泛型编程(GP)、STL、面向对象编程（OOP）、C++之间的关系](https://blog.csdn.net/lsfreeing/article/details/77870275)
5. [Effective Modern C++](https://github.com/kelthuzadx/EffectiveModernCppChinese)
6. [五万字长文总结 C/C++ 知识](https://mp.weixin.qq.com/s/HdfS_pOWJgj3RVuRcVoVWw)
7. [一些著名的软件都用什么语言编写？](https://mp.weixin.qq.com/s/-znPkfMc8f-2hvqCO0-1jQ) (趣味，多数业界软件为了性能，还是采用的C/C++；少部分java)
8. [C++中的抽象类和接口](https://www.programminghunter.com/article/1984129838/)
9. [【C++深度解析】37、C++ 中的抽象类和接口](https://blog.51cto.com/u_15290941/3048773)
10. [C++11 带来的新特性 （3）—— 关键字noexcept](https://www.cnblogs.com/sword03/p/10020344.html)
11. [unordered_map 简介](https://blog.csdn.net/qq_40838478/article/details/114664223)

### 面试参考
- 指针与引用的区别？ 传值参数和传引用参数的差异点？
- 类和结构体的区别？  类的成员默认是private，结构体的成员默认是public；
- C++如何实现多态？ 
- 重载与重写的区别？   
  重载(Overload)：同名的函数，参数等不同；  
  重写(Override)：与虚函数同名同参；基类中同名的虚函数，在子类中被重写；  
  覆盖：非虚同名同参；基类的同名成员在派生类中被屏蔽，被覆盖。
- [腾讯 C++ 笔试/面试题及答案](https://mp.weixin.qq.com/s/1tNQTab8m_CIxaepjwpQig)
