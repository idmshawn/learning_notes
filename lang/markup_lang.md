# 标记语言
最常见的标记语言(markup language)就是HTML，Markdown本身也是一种标记语言。

## XML
拓展标记语言Extensible Markup Language (XML)，经典且使用广泛的标记语言。

##### 格式示例

```
<?xml version="1.0"?>
<sample>
    <languages>Ruby</languages>
    <languages>Perl</languages>
    <languages>Python</languages>
    <websites>
        <element name="YAML">yaml.org</element>
        <element name="Ruby">ruby-lang.org</element>
        <element name="Python">python.org</element>
        <element name="Perl">use.perl.org</element>
    </websites>
</sample>
```

## JSON
JSON(JavaScript Object Notation)是一种由道格拉斯·克罗克福特构想和设计、轻量级的资料交换语言，该语言以易于让人阅读的文字为基础，用来传输由属性值或者序列性的值组成的数据对象。
JavaScript的一个子集，可以直接在JavaScript中解释和编写。尽管JSON是JavaScript的一个子集，但JSON是独立于语言的文本格式，并且采用了类似于C语言家族的一些习惯。JSON数据格式与语言无关。

##### 格式示例

```
{ 
  languages: [ 'Ruby', 'Perl', 'Python'],
  websites: {
    YAML: 'yaml.org',
    Ruby: 'ruby-lang.org',
    Python: 'python.org',
    Perl: 'use.perl.org' 
  } 
}
```
##### 解析支持
Json官网给出多个基于C或C++的解析器，如json-parser；

##### 参考文档
* [JSON官网](https://www.json.org/json-en.html)

## YAML
'YAML Ain't a Markup Language'（YAML不是一种标记语言）的递归缩写，用于跨不同语言和框架的配置文件。
YAML是JSON的超集。理论上，YAML解析器可以理解JSON，但不一定是相反的。
YAML是XML的子集，为XML创建了数据序列化的替代方案。

##### 特点
* 支持锚点(引用)
* 形式简练

##### 格式示例
对象键值对使用冒号结构表示 key: value，冒号后面要加一个空格。
也可以使用 key:{key1: value1, key2: value2, ...}。
还可以使用缩进表示层级关系；
以 - 开头的行表示构成一个数组
```
languages:
  - Ruby
  - Perl
  - Python 
websites:
  YAML: yaml.org 
  Ruby: ruby-lang.org 
  Python: python.org 
  Perl: use.perl.org
```

##### 解析支持
YAML官网给出了libyaml、yaml-cpp等4种基于C/C++的yaml解析器(开源)，供项目快速支持yaml导入。

##### 参考文档
* [阮一峰：YAML语言教程](https://www.ruanyifeng.com/blog/2016/07/yaml.html)
* [YAML官网](https://yaml.org/)

## TOML
YAML的改进及轻量化，适合用于配置文件。官网介绍“A config file format for humans”.
[官网](https://toml.io/en/)也有针对C/C++的开源解析器。

## 比较

网络上关于三者的比较：

[WiKi: Format comparison](https://en.wikipedia.org/wiki/TOML)

    可读性：ini > toml ~ yaml > json > xml
    可以存储的数据复杂度：xml > yaml ~ toml ~ json > ini
    * INI文件：伪二维的文件 , 极其简单。
    * YAML、TOML：二维文件 , 区别在于语法（样子）。
    * JSON：二维文件 , 可读性相对弱 , 无法使用注释 , 不应用于配置文件。现广泛用于数据传输。
    * XML：数据传输和配置文件均可。功能在JSON、YAML之上 , 但是可读性差。

     “要简洁同时功能强大，请用yaml；要在不同语言中交换、共享数据，请用json；想尝鲜，用toml；还不够的话，请用xml吧。”

汇总
||XML|JSON|YAML|
|--|--|--|--|
|适用场景|数据传输和配置文件均可|广泛用于数据传输，Web环境中浏览器和服务器之间的API通信|更多地用于离线数据处理|
|数据复杂度|高|中|中|
|可读性|差|中|好(省去了括号，数据文件大小会小于JSON)|
|存储空间|高|中|低|
|解析器支持||官网链接开源解析器，C/C++多达10+|官网链接开源解析器，C/C++四种|
|解析复杂度||低|高|
|学习难度|低|中|高|

如果作为配置文件，TOML/YAML是较好选择，但也有[反对声音](https://en.wikipedia.org/wiki/TOML)。但如果是WEB编程，JSON是默认方法。

阮一峰对YAML的评价：YAML 是专门用来写配置文件的语言，非常简洁和强大，远比 JSON 格式方便。

缺点：YAML使用空格缩进(同python)。当配置文件过大, 层次过高时, YAML的空格用法将成为危害。（其实 , 编辑器插件就可以解决该问题）

##### 参考
* [比较一下XML, JSON和YAML](https://www.jianshu.com/p/7dbc08ba5ea3)
* [配置文件 INI、YAML、TOML、JSON、XML等比较](https://kyakya.icu/%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6-ini-yaml-toml-json-xml%E7%AD%89%E6%AF%94%E8%BE%83)
* [深入对比TOML，JSON和YAML](https://developer.aliyun.com/article/611301)
