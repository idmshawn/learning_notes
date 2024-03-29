
# 设计原则
## SOLID原则
#### (S)单一职责原则(Single Responsibility Principle, **SRP**) 
There should never be more than one reason for a class to change  
“一个对象应该只包含单一的职责，并且该职责被完整地封装在一个类中”
###### 适用场景
SRP适用于接口、类、方法。接口一定要做到单一职责，类的设计尽量做到只有一个原因引起变化。

#### (O)开闭原则(Open-Closed Principle, **OCP**)
Software entities like classes, modules and functions should be open for extension but closed for modifications.  
软件实现应该对拓展开放，对修改关闭；即，应设计可以在不被修改的前提下易于拓展的模块；

#### (L)里氏替换原则(The Liskov Substitution Principle, **LSP**)
Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.  
“子类应该是可替换父类的，也就是说任何父类可以出现的地方，子类一定可以出现”   
(反之不一定行，有子类出现的地方，父类未必就可以胜任)  
里氏替换包含了4层函数：
1. 子类必须完全实现父类的方法；
2. 子类可以有自己的个性；
3. 子类覆盖或实现父类的方法时输入参数可以被放大；
4. 子类覆写或实现父类的方法时输出结果可以被缩小；

#### (I)接口隔离原则(Interface Segregation Principle, **ISP**)
Clients should not be forced to depend upon interfaces that they dont't use. The dependency of one class to another one should depend on the smallest possible interface.  
“用户不应该被迫依赖他们不使用的方法”，接口要尽量小、接口要高内聚、定制服务、接口设计是有限度的

#### (D)依赖倒置原则(Dependence Inversion Principle, **DIP**)
High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depend upon details. Details should depend upon abstractions.  
高层模块不应该依赖低层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象。

## 其它原则
参考[文档9]  
#### 迪米特法则/最小知识原则(Law of Demeter, aka. Least Knowledge Principle,**LKP**)
Only talk to your immediate friends.  

#### KISS(Keep It Simple and Stupid)原则
美国海军在1960年提出的设计原则。KISS原则指出，大多数系统如果保持简单而不是变得复杂，则效果最佳。因此，简单性应该是设计的主要目标，并且应该避免不必要的复杂性。

#### DRY(Don't Repeat Yourself)原则

# 设计模式
(标题后的星表示难易度，星数量越多越困难)

## 创建型

### 单例模式(Singleton)  :star: 
Ensure a class only has one instance and provide a global point of access to it.

![singleton](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuKhEIImkLWZEp4lFIIt9prEevb9Gq5K0IfTa9YkKvcKMbgPwvW6vUScf41cOIfV4aaG5e90sJ74cL9c69aWKOQH_GMeHK45-7b2YbiiXDIy5Q2y0)

参考[文档12]，两种实现方式下的代码示例：  
- 饿汉模式：指全局的单例实例在类加载时就被构建
```c++
class Singleton
{
public:
  static Singleton &getObject()  // 给外界的唯一接口
  {
    return instance;
  }
  // ...
private:
  Singleton();
  ~Singleton();
  // ...
  static Singleton instance;
};

Singleton Singleton::instance; // 需要在类外定义
```

- 懒汉模式：指全局的单例实例在第一次被使用时构建
```c++
class Singleton
{
public:
  static Singleton &getObject()  // 给外界的唯一接口
  {
    static Singleton instance;
    return instance;
  }
  // ...
private:
  Singleton();
  ~Singleton();
  // ...
};

```

### 工厂方法(Factory Method) :star: :star: :star: 
Define an interface for creating an object, but let subclass decide which class to instantiate. Factory Method lets a classs defer instantiation to subclasses.  
C++代码实现参考[文档8]；但UML图[文档1]或[文档3]更准确，参考下图：
![factory method](https://www.plantuml.com/plantuml/png/nPB1Jkim44Nt_egxV0-KV41ReZP8x118RBjndIcDb7YgyGI4qluxbDGb9IKisKNspVKvcfa7jQ9DNHbNsH1mAsIL1Qq1hWFNzB0biLgo__V_S0IqTXLKhDCz7eMBnkaLxgnJbhTxqWqN7y6zyQo4YjQA2PxEQ-3O1qMBfGVmLRBjFd03tPGXoRwLJhjyZ2LPhtAwz7iJ3TWx8QMZoQ9J-GrrnQfSO_AJKwJc5n8f2qBRqGXf8nwUNayF7niMerZvNs7b4QlqIhAsZc8tPhFJMPPzulM7tL-4WLLqxgpEenUJ-OKaZ8dhDziboN2IezSvZ3cPxD9qm3PwU_XxK9YcKZvlD1k4pPnyqTJLEm00)

工厂方法的**关键在Creator类，或称工厂类**。  
Creator类声明一个抽象的工厂方法FactoryMethod()，返回一个product类的对象；  
SomeOperation()中调用工厂方法创建产品，并可以使用产品的Operation()方法。    
(*代码和UML中的Creator看作Factory，ConcreteCreator看作ConcreteFactory更好理解*)
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
class ConcreteCreatorA : public Creator {
  /**
   * Note that the signature of the method still uses the abstract product type,
   * even though the concrete product is actually returned from the method. This
   * way the Creator can stay independent of concrete product classes.
   */
 public:
  Product* FactoryMethod() const override {
    return new ConcreteProductA();
  }
};
```
工厂方法的调用：
```c++
void ClientCode(const Creator &creator) {
  // ...
  creator.SomeOperation();
  // ...
}

int main() {

  Creator* creator = new ConcreteCreatorA();
  ClientCode(*creator);
  // ...

  delete creator;

  return 0;
}
```

- 符合迪米特法则：高层模块只需要知道产品的抽象类，其它的实现类都不用关心；
- 符合依赖倒置原则：只依赖产品类的抽象；
- 符合里氏替换原则：使用产品子类替换产品父类。
- 开闭原则。无需更改现有客户端代码，你就可以在程序中引入新的产品类型。
- 单一职责原则。你可以将产品创建代码放在程序的单一位置，从而使得代码更容易维护。

###### 使用场景
1. 所有需要生成对象的地方都可以使用，但要能接受增加工厂类增加的代码复杂度。
2. 需要灵活的、可拓展的框架时，可以考虑工厂方法模式；
3. 测试驱动开发(TDD)框架下使用；例如，测试一个类A，就需要把与类A有关联关系的类B也同时产生出来，使用工厂方法把类B虚拟出来，避免类A与类B的耦合。  

### 抽象工厂(Abstract Factory) :star: :star: 
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.  
抽象工厂模式用于**多个工厂**(或产品线)、且每个工厂都能生产**多种类别产品**的二维生产场景。  
对于系列产品的每个变体，都基于抽象工厂接口创建不同的工厂类。**每个工厂类都只能返回特定类别的产品**。

![abs factory](https://www.plantuml.com/plantuml/png/fPF1QeGm48RlUOevAYN2UbmMsKsXr_OLKXr1S1E98wMu--vDkjf2nWYbj-Xy___FZEOyadOqNNjHzteSuRdlq13C0a12gskoxlDuUH_9-VFBuzdNdXvSriQrF1H7UyNN0Pscpfei5tSXEaFel1z2983JwQTMLNEGmwmNvWwrGqtuvcmprNJ9ykDwt0NLBwX2-ZARDPuYN98Fy9ssc_1tr_A_hgpBeh4VfhXLyUO4IowcOOlRslxQJhgauW5NoI7nlam8L4AWl40mSv1XN7chUAii4EGqR98ngjAsYh4fMxNrRNfigQZuZj8etqxCbadRSWVbortkiWo4vB_56KtZB_uN)

抽象工厂的关键在AbstractFactory类和ConcreteFactory类，**ConcreteFactory的方法返回AbstractProduct，方法中实例化ConcreteProduct**：
```c++
/**
 * The Abstract Factory interface declares a set of methods that return
 * different abstract products. These products are called a family and are
 * related by a high-level theme or concept. Products of one family are usually
 * able to collaborate among themselves. A family of products may have several
 * variants, but the products of one variant are incompatible with products of
 * another.
 */
class AbstractFactory {
 public:
  virtual AbstractProductA *CreateProductA() const = 0;
  virtual AbstractProductB *CreateProductB() const = 0;
};

/**
 * Concrete Factories produce a family of products that belong to a single
 * variant. The factory guarantees that resulting products are compatible. Note
 * that signatures of the Concrete Factory's methods return an abstract product,
 * while inside the method a concrete product is instantiated.
 */
class ConcreteFactory1 : public AbstractFactory {
 public:
  AbstractProductA *CreateProductA() const override {
    return new ConcreteProductA1();
  }
  AbstractProductB *CreateProductB() const override {
    return new ConcreteProductB1();
  }
};
```

用户创建ConcreteFactory1和ConcreteFactory2，传入ClientCode；ClientCode中调用工厂的CreateProductA和CreateProductB方法创建具体对象。

###### 使用场景
一个对象族都有相同的约束，则可以使用抽象工厂模式。  
如果代码需要与多个不同系列的相关产品交互， 但是由于无法提前获取相关信息， 或者出于对未来扩展性的考虑， 你不希望代码基于产品的具体类进行构建， 在这种情况下， 你可以使用抽象工厂。

###### 注意事项
缺点：产品族的拓展非常困难。抽象类abstractCreator要增加一个方法createProductC()，两个实现类都要修改，严重违反开闭原则。

### [工厂模式(简单工厂、工厂方法、抽象工厂)比较](https://refactoringguru.cn/design-patterns/factory-comparison)
- 简单工厂模式：描述了一个类，它拥有一个包含大量条件语句的构建方法，可根据方法的参数来选择对何种产品进行初始化并将其返回。  
- 工厂方法：在父类中提供一个创建对象的方法，允许子类决定实例化对象的类型。如果在基类及其扩展的子类中都有一个构建方法的话， 那它可能就是工厂方法。
- 抽象工厂：能创建一系列相关或相互依赖的对象，而无需指定其具体类。  
什么是 “系列对象”？ 例如有这样一组的对象：`运输工具+ 引擎+ 控制器`。 它可能会有几个变体：`汽车+ 内燃机+ 方向盘`，或`飞机+ 喷气式发动机+ 操纵杆`。如果你的程序中并不涉及产品系列的话， 那就不需要抽象工厂。

> 再次重申， 许多人分不清抽象工厂模式和声明为`abstract`的简单工厂。不要犯这个错误！

##### 优缺点比较[文档10、11]：  
- 简单工厂模式下，如果要新增一个产品，就要修改工厂类，不符合开闭原则；可能存在多个if分支，造成代码圈复杂度高。     
- 工厂方法添加了一个抽象的工厂类，新增产品无需修改抽象类；但也存在缺陷：
  - 每新增一个产品，就需要增加一个对应的产品的具体工厂类。相比简单工厂模式而言，工厂方法模式需要更多的类定义。
  - 一条生产线只能一个产品。  
- 抽象工厂类似工厂方法，新增产品，也要增加一个对应的产品的具体工厂类。  
 
##### 简单工厂和工厂方法的适用场景
对于[文档2]的配置解析案例，
> 应用简单工厂“如果不是需要频繁地添加新的parser，只是偶尔修改一下RuleConfigParserFactory代码，稍微不符合开闭原则，也是完全可以接受的”。  
“应用多态或设计模式来替代if分支判断逻辑，也并不是没有任何缺点的，它虽然提高了代码的扩展性，更加符合开闭原则，但也增加了类的个数，牺牲了代码的可读性。”  
实际上，对于规则配置文件解析这个应用场景来说，工厂模式需要额外创建诸多Factory类，也会增加代码的复杂性，而且，每个Factory类只是做简单的new操作，功能非常单薄（只有一行代码），也没必要设计成独立的类，所以，在这个应用场景下，简单工厂模式简单好用，比工厂方法模式更加合适。

推荐使用工厂方法，而非简单工厂的场景：
> 之所以将某个代码块剥离出来，独立为函数或者类，原因是这个代码块的逻辑过于复杂，剥离之后能让代码更加清晰，更加可读、可维护。但是，如果代码块本身并不复杂，就几行代码而已，我们完全没必要将它拆分成单独的函数或者类。  
基于这个设计思想，当对象的创建逻辑比较复杂，不只是简单的new一下就可以，而是要组合其他类对象，做各种初始化操作的时候，我们推荐使用工厂方法模式，将复杂的创建逻辑拆分到多个工厂类中，让每个工厂类都不至于过于复杂。而使用简单工厂模式，将所有的创建逻辑都放到一个工厂类中，会导致这个工厂类变得很复杂。  
除此之外，在某些场景下，如果对象不可复用，那工厂类每次都要返回不同的对象。如果我们使用简单工厂模式来实现，就只能选择第一种包含if分支逻辑的实现方式。如果我们还想避免烦人的if-else分支逻辑，这个时候，我们就推荐使用工厂方法模式。

### 建造者模式(Builder Pattern)(也称生成器模式) :star: :star: :star: 
Separate the construction of a complex object from its representing so that the same construction process can create different representations.

![builder](https://www.plantuml.com/plantuml/png/POzV3i8m28VVEGMF_abli3IBUW3Z3IfZfabj3OKdzUvkYLsYUmI-3_ZrLOEetHF4h2nZ8CQ3nJImODSjFU_n2OXxlCwpywHijl06e1HgnMF99ApSn3KwrpVM2rTBF-ef2fEMvb39LSNeoxI5Bl6eRhVGy7_HsSEzVFiSUix3bEa3)
###### 使用场景
- 相同的方法，不同的执行顺序，产生不同的事件结果时，可使用Builer；
- 多个部件或零件，都可以装配到一个对象中，但是产生的运行结果又不相同时，则可使用Builer；
###### 比较
建造者模式与工厂模式非常相似。  
但Builer最主要功能是基本方法的调用顺序安排，即这些基本方法已经实现了，通俗地说就是零件的装配，顺序不同产生的对象也不同；  
而工厂方法则重点是创建，创建零件是它的主要职责，组装顺序则不是它关心的。  

## 结构型
### 代理模式(Proxy)(也称委托模式) :star: :star: :star: 
Provide a surrogate or placeholder for another object to control access to it.

![proxy](https://www.plantuml.com/plantuml/png/ROvTwi8m4CJVznJx-FyW5v0I2bv0z00bZLkefB7kRa2flRjYRB7guyxCRsTAKSUQkW0-E15SXvQY0hHHYHld2NUfFf1NB8fPinO7GFp7mTMYxBoEo7HA9Fhp2oCyVst9XOdE-I-X3H_FbuTj5i0VtuzAybLzqdae6cFdXV3AczIRw-n1hdaJ9pLGeyOkwbV8r3C9HHKeAUvJ5su0)

代理模式的关键在Proxy类。Proxy类包含一个指向RealSubject对象的引用成员变量。 代理完成其任务（例如延迟初始化、记录日志、访问控制和缓存等）后会将请求传递给RealSubject对象。通常情况下，Proxy会对其RealSubject对象的整个生命周期进行管理。  

核心是Proxy的构造函数：`Proxy(Subject _subject) {this.subject = _subject}`，**你要代理谁就产生该代理的实例，然后把被代理者传递进来**。  
部分示例代码[文档8]：

```c++

class Proxy : public Subject {
 private:
  RealSubject *real_subject_;
  // ...

  /**
   * The Proxy maintains a reference to an object of the RealSubject class. It
   * can be either lazy-loaded or passed to the Proxy by the client.
   */
 public:
  Proxy(RealSubject *real_subject) : real_subject_(new RealSubject(*real_subject)) {
  }

  ~Proxy() {
    delete real_subject_;
  }
  /**
   * The most common applications of the Proxy pattern are lazy loading,
   * caching, controlling the access, logging, etc. A Proxy can perform one of
   * these things and then, depending on the result, pass the execution to the
   * same method in a linked RealSubject object.
   */
  void Request() const override {
      this->real_subject_->Request();
      this->LogAccess();
  }
};

void ClientCode(const Subject &subject) {
  // ...
  subject.Request();
  // ...
}

int main() {

  RealSubject *real_subject = new RealSubject;

  Proxy *proxy = new Proxy(real_subject);
  ClientCode(*proxy);

  // ...
}
```

###### 使用场景
1. RealSubject开销大；或者为第三方库，代码难以修改
RealSubject类处理业务逻辑，但可能性能较慢，占用资源较多，或数据敏感，比如，要校正输入数据；Proxy则可以在不改变RealSubject代码的情况下解决这些问题。Proxy要和RealSubject有完全相同的接口。
2. 减轻Client的负担，屏蔽中间过程，由代理完成“事前调查”和“事后追查”，如现实世界中的打官司找律师代理。

### 桥接模式(Bridge) :star: :star: 
Decouple an abstraction from its implementation so that the two can vary independently. (将抽象和实现解耦，使两者可以独立地变化。)  
桥接模式中，抽象角色(Abstraction)引用实现角色(Implementor)，两者是**组合关系**；模式的**重点是在两者的“解耦”上**。抽象角色的构造函数参数中，传入指定实现角色。     
应用示例：  
- 富翁开公司的例子[文档1]中，“公司”作为抽象角色，“产品”作为实现角色；“产品”可以灵活变更，不会造成“公司”大范围修改。    
- 形状与颜色的例子[文档8]中，通过两者的组合关系，解决子类膨胀的问题。
- GUI和API实现的例子[文档8]中，通过桥接隔离两者的变化。
![bridge](https://www.plantuml.com/plantuml/png/bP0noiCm38LtdKBZ_xVu1Y4axTIrDt0T1GAs76HbIdFt4Z2j0-xGqVBtlGUlIsf5b-31UPiIze-aOfrEaN45n3F6cSJkxxz_s21ZTnedfk58xzyJAybe7U4jp9u2iKR1fddVspRdhZRBswTYTygQQsGdf5HazLd_nRbyTmeAZQTHpUcm0LJZq2opURPOsZMohu00bV4oLfoW8nwMu5y0)

> 桥接模式是一个非常简单的模式，它只是使用了类间的聚合关系、继承、覆写等常用功能，但是它却提供了一个非常清晰、稳定的架构。

###### 使用场景
- 不希望或不适用使用继承的场景
继承属于“强侵入”：父类有一个方法，子类也必须有这个方法。  
- 接口或者抽象类不稳定的场景
- 重用性要求较高的场景

###### 注意事项
使用该模式主要考虑合入拆分抽象和实现。桥接的意图是对变化的封装，尽可能把变化的因素封装到最细、最小的逻辑单元中。  
但并不是一涉及继承就要考虑使用桥接，发现类的继承有N层时，可以考虑使用桥接。  
对于比较明确不发生变化的，则通过继承来完成；若不能确定是否会发生变化，或人为是变化的，则通过桥接模式来解决。  

###### 比较
桥接模式通常会于开发前期进行设计，将程序的各个部分独立开来以便开发。适配器模式通常在已有程序中使用，让相互不兼容的类能很好地合作。  
桥接、 状态模式和策略模式 （在某种程度上包括适配器） 的接口非常相似。 实际上， 它们都基于组合模式，即，将工作委派给其他对象。  

### 装饰者模式(Decorator Pattern)

Attach additional responsibilities to an object dynamically. Provide a flexible alternative to sub-class for extending functionality.

![decorator](https://www.plantuml.com/plantuml/png/VP1B2i8m48RtESKiVP0Rb5BK6tY2CHcnq6RAPEgczku6AWvQSPb_llz1cgmeElQTQvEIN34G7BaVE55IgAgtMjSmEO0zJ7Z9AXXq1Xv8K5jEcwsRdGiTvbpSAGWfMShY-mcVA71HMVv1uPNu2Nl062cU5PLMtl9UpWUwuRrbMV9ia_SxAtVhpNuS_AC64vorhs-sy8knYePIBD_y1000)

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

### 享元模式(Flyweight)
Use Sharing to support large numbers of fine grained objects efficiently.

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
9. [经典永不过时！重温设计模式](http://www.360doc.com/content/21/0601/08/32196507_979923182.shtml)
10. [C++ 深入浅出工厂模式（初识篇）](https://zhuanlan.zhihu.com/p/83535678)
11. [c++设计模式之工厂模式](https://www.cnblogs.com/cxq0017/p/6544517.html)
12. [C++如何实现单例模式](https://blog.csdn.net/liushengxi_root/article/details/79333246)
13. [C++实现单例的5种方法总结](https://blog.csdn.net/zztan/article/details/54691809?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-54691809-blog-79333246.pc_relevant_downloadblacklistv1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-54691809-blog-79333246.pc_relevant_downloadblacklistv1&utm_relevant_index=2)

