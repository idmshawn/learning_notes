# UML

## UML图分类

##### 时序图

##### 状态图

##### 类图
关系

[UML类图的箭头含义](https://www.jianshu.com/p/8969ab8c48c7)
- 泛化(generalization)：继承关系的一种，父类不是抽象类；(空心三角)
- 实现(realize)：继承关系的一种，父类是抽象类；(空心三角)
- 聚合(aggregation)：表示整体由部分构成；(空心菱形)
- 组合(composition)：表示整体由部分构成；(实心菱形)
- 关联(association)：用来定义对象之间静态的、天然的结构；(三角)
- 依赖(dependency)：(三角)

## 工具

### PlantUML

github上的markdwon内嵌plantuml方法，使用PlantUML官网的Online Server存储UML，github中引用存储的外链，示例：

![uml](http://www.plantuml.com/plantuml/png/SyfFKj2rKt3CoKnELR1Io4ZDoSa70000)

### Mermaid

github开源。

PlantText在github上只能使用外链，没法直接使用内嵌语法(实际markdown支持内嵌，但github未支持？)；

Mermaid可以使用内嵌语法；类图关系语法与plantUML类似，其它语法仍有差异？

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

### 参考文档

1. [PlantText](https://www.planttext.com/)：UML在线绘制
2. [PlantUML官网](https://plantuml.com/zh/)：PlantUML语法介绍
3. [mermaid中文说明书(github)](https://github.com/mingcheng/mermaid-gitbook-zh)
4. [mermaid官网](https://mermaid-js.github.io/mermaid/#/)
