# UML

## UML图类型

### 类图
[UML类图中的6大关系](https://blog.csdn.net/ruren1/article/details/81584232?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)

|关系|UML符号|说明|逻辑表示|代码实现|
|--|--|--|--|--|
|**泛化**(Generalization)|实线+空心箭头|就是面向对象语言中的**继承**关系|is a|子类继承父类|
|**实现**(Realization)|虚线+空心箭头|和“泛化”相似，区别在于“实现”继承一个抽象类（abstract、interface），而“泛化”关系继承一个具体类。|is a|**实现接口**或继承某个抽象类|
|聚合(Aggregation)|实线+空心菱形|是整体与部分的关系，部分能脱离整体而独立存在，生命周期不绑定。|has a|成员变量|
|**组合**(Composition)|实线+实心菱形|是整体与部分的关系，但部分不能脱离整体而独立存在，生命周期绑定。|has a|成员变量|
|关联(Association)|实线+箭头|是整体与部分的关系。是一种非常弱的关系，包含聚合、组合两种关系|has a|成员变量|
|关联(Association)|||has many||
|**依赖**(Dependency)|虚线+箭头|是一种使用关系，即一个类的实现需要另一个类的协助。比"关联"更弱的关系，包含"关联"。尽量不使用双向依赖|use a|局部变量、方法的参数和静态方法的调用|

六种关系的耦合度大小是：泛化 = 实现 > 组合 > 聚合 > 关联 > 依赖

![relation](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuIh9BCb9LGXApKaioSpFAyx8B2XMq5LmpaaiBbPmoKnCBqhCvU9A1dCDdstS-sBlCYZFA3Wq3CeqHeYQeAWnHU6PlTYxxaLp7vHd_hHrpTF-7L2UnSlc5I-dhu3oB5ykQdkwVW_CNeFd2ngVjis1SOrVjAzwiR07OR2X2LG15zI92ZOrkhfW5refFDiy-sdFD2vZYB2U7io9LWfFryrxthU1onIgHybGII4Vg4qfDp6lKWdcMYk55uspdaxeu8Aw5wnC2wuCvd0hXUUxMq3Ae4vNiD7LXJiSQ5NhvXUDKxYGdAvWewS7T3XCmPDzSrzidSRba9gN0emL0000)

##### 组合和聚合关系
都表示一对多的has a关系；但生命周期不同(见文档2)：  
> 在组合(Composition)关系中，整体与部分是不可分的，整体的生命周期结束也就意味着部分的生命周期结束。

> 聚合(Aggregation)的整体和部分之间在生命周期上没有什么必然的联系，部分对象可以在整体对象创建之前创建，也可以在整体对象销毁之后销毁。

##### 类的派生和继承关系

类的派生和继承是面向对象程序设计方法和C++语言最重要的特征之一。

> “黑狗就是毛是黑色的狗/黑毛狗”是从一般的dog类通过特殊化而得到类blackDog的。这种通过特殊化已有的类来建立新类的过程，叫做“类的派生”，原有的类叫做“基类”，新建立的类则叫做“派生类”。

> 另一方面，从类的成员的角度来看，派生类自动地将基类地所有成员作为自己的成员，这叫做“继承”。基类和派生类又可以分别叫做“父类”和“子类”，有时也成为“一般类”和“特殊类”。

在C++中，派生（Derive）和继承(inheritance)是一个概念，只是站的角度不同。继承是儿子接收父亲的产业，派生是父亲把产业传承给儿子。

被继承的类称为父类或基类，继承的类称为子类或派生类。“子类”和“父类”通常放在一起称呼，“基类”和“派生类”通常放在一起称呼。

### 时序图

### 状态图


## 工具

### PlantUML

github上的markdwon内嵌plantuml方法，使用PlantUML官网的Online Server存储UML，github中引用存储的外链。  
本地使用时，推荐VScode中安装PlantUML插件。

### Mermaid

PlantText在github上只能使用外链，没法直接使用内嵌语法(实际markdown支持内嵌，但github未支持？)；

Mermaid可以使用内嵌语法？

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

## 参考文档
1. [UML中类之间的六大关系](https://blog.csdn.net/ruren1/article/details/81584232?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)
2. [关联、聚合、组合的区别](https://zhuanlan.zhihu.com/p/359672087)
3. [UML类图的箭头含义](https://www.jianshu.com/p/8969ab8c48c7)
4. [C++继承和派生简明教程](http://c.biancheng.net/view/2264.html)
5. [PlantUML官网](https://plantuml.com/zh/)：PlantUML语法介绍及Online Server
6. [PlantText](https://www.planttext.com/)：UML在线绘制
7. [Mermaid在线绘图](https://mermaid-js.github.io/mermaid-live-editor/)
8. [Mermaid中文说明书(github)](https://github.com/mingcheng/mermaid-gitbook-zh)
9. [Mermaid官网](https://mermaid-js.github.io/mermaid/#/)


----

附：plantUML类图关系源码（github上暂无法直接渲染显示）  
```plantuml
title Relationships - Class Diagram

class 1汽车
class 2SUV
class 3车
class 4汽车
class 5汽车
class 6轮胎
class 7公司
class 8部门
class 9领导
class 10码农
class 13自行车
class 14码农

1汽车 <|-- 2SUV: 泛化(Generalization)
3车 <|.. 4汽车: 接口实现(Interface Realization)
5汽车 o-- 6轮胎: 聚合(Aggregation)
7公司 *-- 8部门: 组合(Composition)
9领导 <-- 10码农: 直接关联(Directed Association)
13自行车 <.. 14码农: 依赖(Dependency)

```

PlantUML类间关系绘制，如组合聚合一对多关系(见文档6的类图示例)   
![relation](http://www.plantuml.com/plantuml/png/XO-xwy8m483t_1L7fj-33Ax5eM872uw2SsY33IPt9G-BgF-x1Wv5yB7b8r--tDKnwP2oTw9pEaPe9kESnHsS1C1_Ymcs5dkQOi43sHxMrEqtWsc8mi-lk0X-k1XrIDvWObvHZeRFI_8-8nC76Kf6YFklyxEwtQ5wv2feSJ319esTUI5o-vjMndadoPc4FvL71T9hF4gUi2hjaQ9Dbl23NLPuTaLjiC_UNG40)
