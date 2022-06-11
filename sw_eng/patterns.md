
# 设计原则

### (S)单一职责原则(Single Responsibility Principle, **SRP**) 
There should never be more than one reason for a class to change  
“一个对象应该只包含单一的职责，并且该职责被完整地封装在一个类中”
###### 适用场景
SRP适用于接口、类、方法。接口一定要做到单一职责，类的设计尽量做到只有一个原因引起变化。

### (O)开闭原则(Open-Closed Principle, **OCP**)
Software entities like classes, modules and functions should be open for extension but closed for modifications.  
软件实现应该对拓展开放，对修改关闭；即，应设计可以在不被修改的前提下易于拓展的模块；

### (L)里氏替换原则(The Liskov Substitution Principle, **LSP**)
Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.  
“子类应该是可替换父类的，也就是说任何父类可以出现的地方，子类一定可以出现”   
(反之不一定行，有子类出现的地方，父类未必就可以胜任)  
里氏替换包含了4层函数：
1. 子类必须完全实现父类的方法；
2. 子类可以有自己的个性；
3. 子类覆盖或实现父类的方法时输入参数可以被放大；
4. 子类覆写或实现父类的方法时输出结果可以被缩小；

### (I)接口隔离原则(Interface Segregation Principle, **ISP**)
Clients should not be forced to depend upon interfaces that they dont't use. The dependency of one class to another one should depend on the smallest possible interface.  
“用户不应该被迫依赖他们不使用的方法”，接口要尽量小、接口要高内聚、定制服务、接口设计是有限度的

### (D)依赖倒置原则(Dependence Inversion Principle, **DIP**)
High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depend upon details. Details should depend upon abstractions.  
高层模块不应该依赖低层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象。


### 迪米特法则(Law of Demeter, aka. Least Knowledge Principle,**LKP**)
Only talk to your immediate friends.  


# 设计模式
(标题后的星表示难易度，星数量越多越困难)

## 创建型

### 单例模式(Singleton)  :star: 

### 工厂方法(Factory Method) :star: :star: :star: 
Define an interface for creating an object, but let subclass decide which class to instantiate. Factory Method lets a classs defer instantiation to subclasses.  
C++代码实现参考[文档8]；但UML图[文档1]或[文档3]更准确，参考下图：
![factory method](https://www.plantuml.com/plantuml/png/nPB1Jkim44Nt_egxV0-KV41ReZP8x118RBjndIcDb7YgyGI4qluxbDGb9IKisKNspVKvcfa7jQ9DNHbNsH1mAsIL1Qq1hWFNzB0biLgo__V_S0IqTXLKhDCz7eMBnkaLxgnJbhTxqWqN7y6zyQo4YjQA2PxEQ-3O1qMBfGVmLRBjFd03tPGXoRwLJhjyZ2LPhtAwz7iJ3TWx8QMZoQ9J-GrrnQfSO_AJKwJc5n8f2qBRqGXf8nwUNayF7niMerZvNs7b4QlqIhAsZc8tPhFJMPPzulM7tL-4WLLqxgpEenUJ-OKaZ8dhDziboN2IezSvZ3cPxD9qm3PwU_XxK9YcKZvlD1k4pPnyqTJLEm00)

工厂方法的关键在Creator类。  
Creator类声明一个抽象的工厂方法FactoryMethod()，返回一个product类的对象；  
SomeOperation()中调用工厂方法创建产品，并可以使用产品的Operation()方法。    
```c++
class Creator {
  /**
   * Note that the Creator may also provide some default implementation of the
   * factory method.
   */
 public:
  virtual ~Creator(){};
  virtual Product* FactoryMethod() const = 0;
  /**
   * Also note that, despite its name, the Creator's primary responsibility is
   * not creating products. Usually, it contains some core business logic that
   * relies on Product objects, returned by the factory method. Subclasses can
   * indirectly change that business logic by overriding the factory method and
   * returning a different type of product from it.
   */

  std::string SomeOperation() const {
    // Call the factory method to create a Product object.
    Product* product = this->FactoryMethod();
    // Now, use the product.
    std::string result = "Creator: The same creator's code has just worked with " + product->Operation();
    delete product;
    return result;
  }
};
```

Creator的子类实现具体的工厂方法，返回不同类型的product对象。  
```c++
/**
 * Concrete Creators override the factory method in order to change the
 * resulting product's type.
 */
class ConcreteCreator1 : public Creator {
  /**
   * Note that the signature of the method still uses the abstract product type,
   * even though the concrete product is actually returned from the method. This
   * way the Creator can stay independent of concrete product classes.
   */
 public:
  Product* FactoryMethod() const override {
    return new ConcreteProduct1();
  }
};
```

- 符合迪米特法则：高层模块只需要知道产品的抽象类，其它的实现类都不用关心；
- 符合依赖倒置原则：只依赖产品类的抽象；
- 符合里氏替换原则：使用产品子类替换产品父类。
- 开闭原则。无需更改现有客户端代码，你就可以在程序中引入新的产品类型。
- 单一职责原则。你可以将产品创建代码放在程序的单一位置，从而使得代码更容易维护。

###### 使用场景
1. 工厂方法是new一个对象的替代品，所有需要生成对象的地方都可以使用。
2. 需要灵活


### 抽象工厂(Abstract Factory)



[工厂模式(简单工厂、工厂方法、抽象工厂)比较](https://refactoringguru.cn/design-patterns/factory-comparison)

### 构建者模式(Builder Pattern)(也称生成器模式) :star: :star: :star: 
separate the construction of a complex object from its representation so that the same construction process can create different representations.
###### 使用场景
- 相同的方法，不同的执行顺序，产生不同的事件结果时，可使用Builer；
- 多个部件或零件，都可以装配到一个对象中，但是产生的运行结果又不相同时，则可使用Builer；
###### 比较
建造者模式与工厂模式非常相似。  
但Builer最主要功能是基本方法的调用顺序安排，即这些基本方法已经实现了，通俗地说就是零件的装配，顺序不同产生的对象也不同；  
而工厂方法则重点是创建，创建零件是它的主要职责，组装顺序则不是它关心的。  

## 结构型
### 代理模式(Proxy)
### 适配器模式(Adapter Pattern)(也称包装模式, wrapper) :star: :star: 
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.  
(将一个类的接口变换成用户所期待的另一种接口，从而使原本因接口不匹配而无法在一起工作的两个类能够在一起工作)
###### 使用场景
类似于笔记本的110V~220V电源适配器，引入一个转换对象，用于把一个接口或类转换后，可对接其它接口或类。
###### 注意事项
适配器是一个“补救”模式。软件设计阶段最好不要使用此模式，它不是为了解决还在开发阶段的问题，而是为了解决正在服役的项目问题。  
项目一定要遵循依赖倒置和里氏替换原则，否则即使再适合使用适配器的场合下，也会迎来大的改造。

### 门面模式(Facade Pattern)(也称外观模式) :star: :star: 
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.  
用户只看到一个门面类，不感知复杂的内部细节；

## 行为型
### 策略模式(Strategy Pattern)(也称政策模式, Policy) :star: :star: :star: 
Define a family of algorithms, encapsulate each one, and make them interchangealbe.  
(定义一组算法，将每个算法都封装起来，并且使它们之间可以互换)  
###### 使用场景
- 多个类只有在算法或行为上稍有不同的场景；
- 算法需要自由切换的场景；
- 需要屏蔽算法规则的场景；

### 观察者模式(Observer)(也称发布订阅模式,Publish/subscribe) :star: :star: :star: 
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.  
(定义对象间一种一对多的依赖关系，使得每当一个对象改变状态，则所有依赖于它的对象都会得到通知并被自动更新)  
实际是将主控监控观察按照被动等通知(订阅)实现。
###### 使用场景
- 关联行为场景；关联行为是可拆分的，而不是“组合”关系。
- 事件多级触发场景；
- 跨系统的消息交互场景，如消息队列的处理机制。

### 访问者模式(Visitor Pattern) :star: :star: :star: :star: :star: 
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.
###### 使用场景

### 模板方法模式(Template Method Pattern)  :star: 
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.
###### 使用场景
- 多个子类有公有的方法，并且逻辑基本相同时；
- 重要、复杂的算法，可以把核心算法设计为模板方法，周边的相关细节功能则由各个子类实现；
- 重构时的常用模式，把相同的代码抽取到父类中，然后通过钩子函数(见“模板方法模式的拓展”)约束其行为。

## 拓展
### 基于贫血模型的MVC三层架构开发模式
MVC(Model-View-Controller)三层架构已经成为标准的Web项目的开发模式，但它却违反了OOP。  
只包含数据，不包含业务逻辑的类，就叫作贫血模型（Anemic Domain Model）。  
这种贫血模型将数据与操作分离，破坏了面向对象的封装特性，是一种典型的面向过程的编程风格。

### 基于充血模型的DDD开发模式
充血模型（Rich Domain Model）正好相反，数据和对应的业务逻辑被封装到同一个类中。  
基于贫血模型的传统的开发模式，比较适合业务比较简单的系统开发。  
相对应的，基于充血模型的DDD开发模式，更适合业务复杂的系统开发。比如，包含各种利息计算模型、还款模型等复杂业务的金融系统。

# 设计模式应用
书籍或教程中提及的设计模式
### 附1，《领域驱动设计》中提到的设计模式
- 策略模式(Strategy)：p36，ch1.4
- 外观模式(Facade)：p59，ch3.2； p91，ch5.4.1, p279, ch14.8.2
- 观察者模式(Observers)：p68, ch4.1.1
- 适配器模式(Adapter)：p279, ch14.8.2
- 工厂模式(Factory)、抽象工厂：p113, ch6.2
- 构建器模式(Builder)：p113, ch6.2
### 附2，《重构》中提到的设计模式
- 生成器(Builder)：重构MOOC课程.ppt p41
- 策略(stategy)：重构MOOC课程.ppt p45, 重构2 p330
- 单例(singleton): 重构2 p318
- 访问者(visitor)：重构2 p330
- 模板方法(template method)：重构MOOC课程.ppt p33
### 附3，常用与不常用的设计模式
[《设计模式之美》](https://time.geekbang.org/column/intro/100039001)中提到的“常用”与“不常用”设计模式。
>1.创建型  
常用的有：单例模式、工厂模式（工厂方法和抽象工厂）、建造者模式。  
不常用的有：原型模式。  
2.结构型  
常用的有：代理模式、桥接模式、装饰者模式、适配器模式。  
不常用的有：门面模式、组合模式、享元模式。  
3.行为型  
常用的有：观察者模式、模板模式、策略模式、职责链模式、迭代器模式、状态模式。  
不常用的有：访问者模式、备忘录模式、命令模式、解释器模式、中介模式。  


# 参考
1. 设计模式之禅(第2版), 秦小波 
2. 极客时间课程[《设计模式之美》-王争](https://time.geekbang.org/column/intro/100039001)  
3. [Design Patterns Cards](http://www.mcdonaldland.info/files/designpatterns/designpatternscard.pdf)(设计模式记忆卡片)
4. [写了这么多年代码，你真的了解设计模式么](https://insights.thoughtworks.cn/do-you-really-know-design-pattern/)
5. [写了这么多年代码，你真的了解SOLID吗](https://insights.thoughtworks.cn/what-is-solid-principle/)
6. [Github: Design Patterns For Humans](https://github.com/Leon0X/design-patterns-for-humans-cn)
7. [设计模式C++11实现](https://github.com/jaredtao/DesignPattern)
8. [Refactoring Guru:设计模式](https://refactoringguru.cn/design-patterns/catalog)

