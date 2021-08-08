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




# CleanCode

引言：[重构要首先识别代码坏味道](https://github.com/MagicBowen/refactoring/blob/master/effective-refactoring-1.md#%E5%85%B3%E4%BA%8E%E6%9C%AC%E6%96%87)

### 提升可读性

### 消除重复

### 耦合？

