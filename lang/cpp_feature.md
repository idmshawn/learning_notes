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

#### new和delete
new operator/delete operator就是new和delete**操作符**(C++ Primer中称为new表达式)，而operator new/operator delete是**函数**。 [详见[文档6](https://www.cnblogs.com/luxiaoxun/archive/2012/08/10/2631812.html)]

new 、operator new 和 placement new 区别  
1. new operator(或称new表达式)：不能被重载，其行为总是一致的。它先调用operator new分配内存，然后调用构造函数初始化那段内存。  
  new 操作符的执行过程：
    - 调用operator new分配内存 ；
    - 调用构造函数生成类对象；
    - 返回相应指针。
2. operator new：要实现不同的内存分配行为，应该重载operator new，而不是new。  
operator new就像operator + 一样，是可以重载的。如果类中没有重载operator new，那么调用的就是全局的::operator new来完成堆的分配。同理，operator new[]、operator delete、operator delete[]也是可以重载的。
    - 只分配所要求的空间，不调用相关对象的构造函数。当无法满足所要求分配的空间时，则  
        ->如果有new_handler，则调用new_handler，否则  
        ->如果没要求不抛出异常（以nothrow参数表达），则执行bad_alloc异常，否则  
        ->返回0  
    - 可以被重载
    - 重载时，返回类型必须声明为void*
    - 重载时，第一个参数类型必须为表达要求分配空间的大小（字节），类型为size_t
    - 重载时，可以带其它参数
3. placement new：只是operator new重载的一个版本。它并不分配内存，只是返回指向已经分配好的某段内存的一个指针。因此不能删除它，但需要调用对象的析构函数。  
如果你想在已经分配的内存中创建一个对象，使用new时行不通的。也就是说placement new允许你在一个已经分配好的内存中（栈或者堆中）构造一个新的对象。原型中void* p实际上就是指向一个已经分配好的内存缓冲区的的首地址。[placement new使用场景](https://www.geeksforgeeks.org/placement-new-operator-cpp/)。

new operator(C++ Primer中称为new表达式)与delete operator的行为是不能够也不应该被改变，这是C++标准作出的承诺。而operator new与operator delete和C语言中的malloc与free对应，只负责分配及释放空间。但使用operator new分配的空间必须使用operator delete来释放，而不能使用free，因为它们对内存使用的登记方式不同。反过来亦是一样。

综上，**new表达式是分配内存+调用构造；operator new仅分配内存，不调用构造；placement new仅调用构造，不分配内存(使用传入的内存地址)**[C++ Primer 19.1.2节]。

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

### 接口和抽象类(C++实现)
抽象类更多的是为了代码复用，而接口就更侧重于解耦。  
"我们可以使用接口来实现面向对象的抽象特性、多态特性和基于接口而非实现的设计原则；使用抽象类来实现面向对象的继承特性和模板设计模式等。"  
设计模式书籍或很多类图中，会有类标以《Interface》或《Abstract》，即标识的接口和抽象类。  
Java直接使用Interface和Abstract关键字定义接口类和抽象类，C++没有这种关键字，但可以间接实现这两个功能。  
##### 抽象类
OOP中的抽象类：
- 是一种只能定义类型，而不能产生对象(实例化)的类；  
- 只能被继承，并重写相关函数；(子类继承抽象类，必须实现抽象类中的所有抽象方法)  

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
Shape: +area()

class Rect{
  -int a
  -int b
  +area()
}
class Circle{
  -int r
  +area()
}
```

``` c++
class Shape {
public:
    virtual double area() = 0;  // 抽象类定义纯虚函数
};

class Rect : public Shape {
public:
    // ...

    double area() { // 子类重写纯虚函数
        // ...
    }
};
```

##### 接口
C++使用抽象类实现接口。满足下面条件的C++类称为接口
- 类中没有定义任何变量；(接口不能包含属性，也就是成员变量)  
- 所有的成员函数都是纯虚函数，且是公有的；(接口只能声明方法，方法不能包含代码实现)
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

##### 如何决定该用抽象类还是接口？
如果一个类是父类，就要考虑它有没有必要成为一个抽象类，判断准则是这个父类有没有必要产生一个对象，没必要则做成抽象类。  
“如果我们要表示一种is-a的关系，并且是为了解决代码复用的问题，我们就用抽象类；  
如果我们要表示一种has-a关系，并且是为了解决抽象而非代码复用的问题，那我们就可以使用接口。”  
“从类的继承层次上来看，抽象类是一种自下而上的设计思路，先有子类的代码重复，然后再抽象成上层的父类（也就是抽象类）。  
而接口正好相反，它是一种自上而下的设计思路。我们在编程的时候，一般都是先设计接口，再去考虑具体的实现。”

## 参考
1. C++手册：[cppreference](https://en.cppreference.com/w/)
2. [C++那些事](https://light-city.club/sc/)
3. [C++ STL与泛型编程（三）](https://blog.csdn.net/zl6481033/article/details/89465421?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control&dist_request_id=1328665.10354.16159908009496807&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control)
4. [泛型编程、STL的概念、STL模板思想及其六大组件的关系，以及泛型编程(GP)、STL、面向对象编程（OOP）、C++之间的关系](https://blog.csdn.net/lsfreeing/article/details/77870275)
5. [Effective Modern C++](https://github.com/kelthuzadx/EffectiveModernCppChinese)
6. [C++中的new、operator new与placement new](https://www.cnblogs.com/luxiaoxun/archive/2012/08/10/2631812.html)
7. [一些著名的软件都用什么语言编写？](https://mp.weixin.qq.com/s/-znPkfMc8f-2hvqCO0-1jQ) (趣味，多数业界软件为了性能，还是采用的C/C++；少部分java)
8. [C++中的抽象类和接口](https://www.programminghunter.com/article/1984129838/)
9. [【C++深度解析】37、C++ 中的抽象类和接口](https://blog.51cto.com/u_15290941/3048773)

### 面试参考
- 指针与引用的区别？ 传值参数和传引用参数的差异点？
- 类和结构体的区别？  类的成员默认是private，结构体的成员默认是public；
- C++如何实现多态？ 
- 重载与重写的区别？   
  重载(Overload)：同名的函数，参数等不同；  
  重写(Override)：与虚函数同名同参；基类中同名的虚函数，在子类中被重写；  
  覆盖：非虚同名同参；基类的同名成员在派生类中被屏蔽，被覆盖。
- [腾讯 C++ 笔试/面试题及答案](https://mp.weixin.qq.com/s/1tNQTab8m_CIxaepjwpQig)
