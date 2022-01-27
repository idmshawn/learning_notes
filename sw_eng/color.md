# 彩色UML建模(四色原型)(Object Modeling in Color)

## 基本概念
DDD领域模型建模推荐使用四色模型。  
四色建模法是在UML建模的基础上增添了一些描述，把实体分为四类，并标注不同的颜色的一种建模方法。

|颜色|含义及缩写|说明|备注|
|--|--|--|--|
|绿|Part-Place-Thing, PPT|人/事/物，表示参与某个活动的人或物，地点则是活动的发生地||
|黄|Role|PPT参与活动的方式，就是我们平时所理解的“身份”|可理解为动作|
|粉|Moment-Interval, MI|时标性对象，表示在某个时刻或某一段时间内发生的某个活动|可理解为状态|
|蓝|Description, DESC|表示对PPT的本质描述||

MI写法一般是名词+动词的被动态，比如Command Executed。

> 用一句话来概括四色原型就是：一个什么什么样的人或组织或物品以某种角色在某个时刻或某段时间内参与某个活动。  
 其中“什么什么样的”就是DESC，  
“人或组织或物品”就是PPT，  
“角色”就是Role，  
而”某个时刻或某段时间内的某个活动"就是MI。  

## 建模工具
[基于PlantUML 的4色 领域模型建模](https://gitee.com/xhector/coloruml)

## 参考
1. [WikiPedia:Object Modeling in Color](https://en.wikipedia.org/wiki/Object_Modeling_in_Color)
2. [DDD-领域模型-四色原型](https://blog.csdn.net/wuzxc520/article/details/78897135)
