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

## 组合(Composition)

``` c++
// 组合关系：整体与部分的关系，但是整体与部分不可以分开
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

## 聚合
``` c++
// 聚合关系, 整体和部分的关系，整体与部分可以分开
class Wheel {
public:
  Wheel() {};
  ~Wheel() {};
};

class Car {
public:
  Car() {};
  ~Car() {};
  void SetWheel(Wheel *front, Wheel *rear)  // 生命周期不绑定，通过set方法或者构造函数赋值到本类
  {
    this.frontWheel = front;
    this.rearWheel = rear;
  }
private:
  Wheel *frontWheel;
  Wheel *rearWheel;
};

```

## 依赖(Dependency)

##### C++


##### C语言



## 参考
1. [UML类图（下）：关联、聚合、组合、依赖](https://www.cnblogs.com/xrq730/p/5533019.html)
2. [Java 代码表示 UML 依赖/泛化/实现/关联/聚合/组合关系](https://www.zhangbj.com/p/478.html)
