
# 设计原则

|序号|原则|缩写|原文|描述|使用场景|
|--|--|--|--|--|--|
|1|单一职责原则|Single Responsibility Principle, **SRP**|There should never be more than one reason for a class to change|||
|2|里氏替换原则|Liskov Substitution Principle, **LSP**|Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.|||
|3|依赖倒置原则|Dependence Inversion Principle, **DIP**|High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depend upon details. Details should depend upon abstractions.|||
|4|接口隔离原则|**ISP**|Clients should not be forced to depend upon interfaces that they dont't use. The dependency of one class to another one should depend on the smallest possible interface.|||
|5|迪米特法则|Law of Demeter, LoD(Least Knowledge Principle,LKP)|Only talk to your immediate friends.|||
|6|开闭原则|open Close Principle, **OCP**|Software entities like classes, modules and functions should be open for extension but closed for modifications.|||


# 设计模式

### 结构模式
代理模式(Proxy)
适配器模式(Adapter)
工厂(Factory)
抽象工厂(Abstract Factory)
门面模式(Facade)

### 创建模式
工厂模式(Factory Method)
单例模式(Singleton)
构建者模式(Builder)

### 行为模式
策略模式(Strategy)
观察者模式(Observer)


### 参考
1. 设计模式之禅(第2版), 秦小波 
2. [写了这么多年代码，你真的了解设计模式么](https://insights.thoughtworks.cn/do-you-really-know-design-pattern/)
3. [写了这么多年代码，你真的了解SOLID吗](https://insights.thoughtworks.cn/what-is-solid-principle/)
