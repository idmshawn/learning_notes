# 类与类交互关系的代码实现

## 泛化(Generalization)/继承(Inheritance)

``` c++
class Car {
public:
  Car() {};
  ~Car() {};
  void Run() {
    // ...
  }
};

// 子类SUV继承父类Car
class SUV : public Car {
public:
  SUV() {};
  ~SUV() {};
  void Run() { // 继承父类的方法，覆盖父类的实现
    // ...
  }
};
```

## 实现(Realization)
实现接口或继承某个抽象类 

``` c++
// 抽象类Vehicle
class Vehicle {
public:
  Vehicle() {};
  ~Vehicle() {};
  virtual void Run() = 0;  // 定义纯虚函数
};

// 子类Car实现抽象类Vehicle
class Car : public Vehicle {
public:
  Car() {};
  ~Car() {};
  void Run() { // 子类重写纯虚函数
    // ...
  }
};
```

## 聚合(Aggregation)
整体和部分的关系，整体与部分可以分开。  
聚合关系代码一般实现方式：A类的对象在创建时，不会立即创建B类的对象，而是等待一个外界的对象传给它。  
``` c++
class Wheel {
public:
  Wheel() {};
  ~Wheel() {};
};

class Car {
public:
  Car() {};
  ~Car() {};
  void SetWheel(Wheel *front, Wheel *rear)  // 生命周期不绑定，通过set方法或者构造函数赋值到Car类
  {
    this.frontWheel = front;
    this.rearWheel = rear;
  }
private:
  Wheel *frontWheel;
  Wheel *rearWheel;
};
```

## 组合(Composition)
整体与部分的关系，但是整体与部分不可以分开。
组合关系代码一般实现方式：A类的构造方法里创建B类的对象，也就是说，当A类的一个对象产生时，B类的对象随之产生，当A类的这个对象消亡时，它所包含的B类的对象也随之消亡。 
``` c++
class Department {
public:
  Department() {};
  ~Department() {};
};

class Company {
public:
  Company() {
    departmentA = new Department;  // 生命周期绑定，直接new
    departmentB = new Department;
  };
  ~Company() {};

private:
  Department departmentA;
  Department departmentB;
};
```

## 关联(Association)
关联与聚合仅仅从 Java 或 C++ 语法上是无法分辨的，必须考察所涉及的类之间的逻辑关系。
组合关系代码一般实现：一个类作为另一个类方法的参数。
``` c++
class A{
  //...
};
class B{
  //...
};
A::Function1(B &b); 
//或A::Function1(B b);
//或A::Function1(B *b);
```

## 依赖(Dependency)
使用关系。  
UML中，依赖关系用带箭头的虚线表示，由依赖的一方指向被依赖的一方。[文档2]
``` c++
class Bicycle {
public:
  Bicycle() {};
  ~Bicycle() {};
  void move();
};

class Men {
public:
  Men() {};
  ~Men() {};
  void Go(Bicycle &bicycle)  // 将一个类的对象作为另一个类中方法的参数
  {
    bicycle.move();
  }
};
```

## 参考
1. [c++uml关系总结](https://www.daimajiaoliu.com/daima/47192348b900403)
2. [UML类图（下）：关联、聚合、组合、依赖](https://www.cnblogs.com/xrq730/p/5533019.html)
3. [Java 代码表示 UML 依赖/泛化/实现/关联/聚合/组合关系](https://www.zhangbj.com/p/478.html)

