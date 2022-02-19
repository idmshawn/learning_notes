# 类与类交互关系的代码实现

## 泛化(Generalization)/继承(Inheritance)

##### C++
``` c++
// 具体类Car
class Car {
public:
  Car() {};
  ~Car() {};
  void Run() {
    // ...
  }
};

// 子类SUV为父类Car的泛化
class SUV : public Car {
public:
  SUV() {};
  ~SUV() {};
  void Run() { // 覆盖父类的实现
    // ...
  }
};
```

##### C语言

## 实现(Realization)
实现接口或继承某个抽象类 
##### C++
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
##### C语言

## 组合(Composition)
生命周期绑定

##### C++
``` c++
class Department {
public:
  Department() {};
  ~Department() {};
};

class Company {
public:
  Company() {};
  ~Company() {};
private:
  Department departmentA;  // 生命周期绑定
  Department departmentB;
  Department departmentC;
};

```
##### C语言

## 聚合
``` c++
class Tires {
public:
  Tires() {};
  ~Tires() {};
};

class Car {
public:
  Car() {};
  ~Car() {};
private:
  Tires *tires;  // 生命周期不绑定
};

```

## 依赖(Dependency)

##### C++


##### C语言
