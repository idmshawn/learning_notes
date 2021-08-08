# 简单设计

演进式设计原则： 
保持简单  --》 简单设计

软件设计的核心是降低“偶发成本(Incidental Cost)”，使得成本趋近于内在成本；

### 偶发成本来源
重复带来偶发成本：
- 确保一致性的成本；
- 散弹式修改带来的成本；
- 测试范围扩大带来的成本；

难以理解带来的偶发成本：
- 不知道在哪里修改
- 不知道怎么修改
- -》
- 沟通、溯源成本
- 理解错误导致修改错误引入更大的成本

冗余带来偶发成本
- 思维负担
- **过度设计**可引入冗余代码
（当前静态检查工具控制的较好）

### 简单设计原则
(Kent Beck提出)
1. 通过所有测试（Passes its tests）
2. 尽可能消除重复 (Minimizes duplication)：代码可复用度高
3. 尽可能清晰表达 (Maximizes clarity)
4. 更少代码元素 (Has fewer elements) :  避免过度设计
以上四个原则的重要程度依次降低。

四原则同样可评判领域建模等软件相关设计xx


# 开发者测试
简单设计的衡量标尺；

70年代图灵奖获得者Edsger W. Dijkstra：“测试只能证明程序的错误，但是永远不能证明程序是正确的”。

开发者测试两种常见办法：
- 系统实现后补充测试你；
- 测试写出，再把系统实现；(也称测试驱动开发)

TDD优势：站在用户角度设计API；而不是像前者站在实现角度，系统实现和测试用例会出现相互耦合；

### 测试驱动开发(TDD)
Kent Beck书籍: Test-Driven Development 

TDD三定律(TDD cyclye)：
liuguangcong解释不清晰，建议再参考以下解释：
- [Test-Driven Development (TDD) – Quick Guide](https://brainhub.eu/blog/test-driven-development-tdd/)
- [Test-Driven Development (TDD)](https://docs.firstdecode.com/tdd/)

### 测试替身(TestDouble)
概念来自《xUnit Test Patterns》。敏捷开发最基础的工程实践是“持续集成”和“单元测试“。
xUnit Test Patterns一书主要就是介绍作者在实践“单元测试”过程中碰到的许多问题及其解决之道。

SUT(system under test)：被测对象；

##### 测试替身有以下几类
- Dummy object, 占位符；
- Test Stub，测试桩；
- Test Spy；
- Mock Object；
- Fake Object；

##### 测试替身的替换时机
- Preprocessor substitution(预编译期替换)：宏实现多态，依赖函数定义为一个宏，真实场景和测试场景做不同宏实现。
- Compile-time substitution(编译期替换)：template实现多态，真实场景和测试场景传不同的模板特化版本；
- Link-time substitution(链接期替换)：借助makefile或构建脚本，真实场景和测试场景链接不同的函数符号；
- Running-time substitution(运行期替换)：函数指针挂接，不同场景挂接的实现不同；

时机选择遵循**最小侵入**原则。


# CleanCode

引言：[重构要首先识别代码坏味道](https://github.com/MagicBowen/refactoring/blob/master/effective-refactoring-1.md#%E5%85%B3%E4%BA%8E%E6%9C%AC%E6%96%87)

### 提升可读性

### 消除重复

### 耦合？

