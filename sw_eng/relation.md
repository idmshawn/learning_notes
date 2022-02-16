# 类与类交互关系的代码实现

## 泛化(Generalization)

##### C++
``` c++

// 具体类Car
class Car {
public:
  Car() {}
  ~Car() {}
  void Run() {
    // ...
  }
};

// 子类SUV为父类Car的泛化
class SUV : public Car {
public:
  SUV() {}
  ~SUV() {}
  void Run() { // 覆盖父类的实现
    // ...
  }
};
```

##### C语言

## 实现(Realization)

##### C++
``` c++

// 抽象类Vehicle
class Vehicle {
public:
  Vehicle() {}
  ~Vehicle() {}
  virtual void Run() = 0;  // 定义纯虚函数
};

// 子类Car实现抽象类Vehicle
class Car : public Vehicle {
public:
  Car() {}
  ~Car() {}
  void Run() { // 子类重写纯虚函数
    // ...
  }
};


```
##### C语言

## 组合(Composition)

##### C++
##### C语言

## 依赖(Dependency)

##### C++
##### C语言
