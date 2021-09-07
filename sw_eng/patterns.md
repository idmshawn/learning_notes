
# 设计原则

|序号|原则|缩写|原文|描述|使用场景|
|--|--|--|--|--|--|
|S|单一职责原则|Single Responsibility Principle, **SRP**|There should never be more than one reason for a class to change|||
|O|开闭原则|Open-Closed Principle, **OCP**|Software entities like classes, modules and functions should be open for extension but closed for modifications.|||
|L|里氏替换原则|The Liskov Substitution Principle, **LSP**|Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.|||
|I|接口隔离原则|Interface Segregation Principle, **ISP**|Clients should not be forced to depend upon interfaces that they dont't use. The dependency of one class to another one should depend on the smallest possible interface.|||
|D|依赖倒置原则|Dependence Inversion Principle, **DIP**|High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depend upon details. Details should depend upon abstractions.|||
| |迪米特法则|Law of Demeter, LoD(Least Knowledge Principle,LKP)|Only talk to your immediate friends.|||

# 设计模式
(标题后的星表示难易度，星数量越多越困难)

## 结构模式
### 代理模式(Proxy)
### 适配器模式(Adapter)
### 工厂(Factory)
### 抽象工厂(Abstract Factory)

### 门面模式(Facade Pattern)(也称外观模式) :star: :star: 
###### 定义
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
用户只看到一个门面类，不感知复杂的内部细节；

## 创建模式
### 工厂模式(Factory Method)
### 单例模式(Singleton)  :star: 
### 构建者模式(Builder Pattern)(也称生成器模式) :star: :star: :star: 
###### 定义
separate the construction of a complex object from its representation so that the same construction process can create different representations.
###### 使用场景
- 相同的方法，不同的执行顺序，产生不同的事件结果时，可使用Builer；
- 多个部件或零件，都可以装配到一个对象中，但是产生的运行结果又不相同时，则可使用Builer；
###### 比较
建造者模式与工厂模式非常相似。  
但Builer最主要功能是基本方法的调用顺序安排，即这些基本方法已经实现了，通俗地说就是零件的装配，顺序不同产生的对象也不同；  
而工厂方法则重点是创建，创建零件是它的主要职责，组装顺序则不是它关心的。  

## 行为模式
### 策略模式(Strategy Pattern) :star: :star: :star: 
###### 定义
Define a family of algorithms, encapsulate each one, and make them interchangealbe.
一个抽象的stategy接口，对应3~5个不同的策略；

### 观察者模式(Observer)

### 访问者模式(Visitor Pattern)
###### 定义
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.
###### 使用场景


### 模板方法模式(Template Method Pattern)  :star: 
###### 定义
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.
###### 使用场景
- 多个子类有公有的方法，并且逻辑基本相同时；
- 重要、复杂的算法，可以把核心算法设计为模板方法，周边的相关细节功能则由各个子类实现；
- 重构时的常用模式，把相同的代码抽取到父类中，然后通过钩子函数(见“模板方法模式的拓展”)约束其行为。


# 参考
1. 设计模式之禅(第2版), 秦小波 
2. [Design Patterns Cards](http://www.mcdonaldland.info/files/designpatterns/designpatternscard.pdf)(设计模式记忆卡片)
3. [写了这么多年代码，你真的了解设计模式么](https://insights.thoughtworks.cn/do-you-really-know-design-pattern/)
4. [写了这么多年代码，你真的了解SOLID吗](https://insights.thoughtworks.cn/what-is-solid-principle/)
