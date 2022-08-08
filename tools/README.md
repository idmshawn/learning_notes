# UML工具

PlantUML和Mermaid都支持以“代码”的方式绘制UML图，含类图、时序图、状态图等。两者语法不完全相同。  
- 前者尚未在github上支持嵌入，需引用外链；但其图形标识好于后者，比如类有“C”标识。  
- 后者已支持github嵌入，但图形标识过于简单，尤其是类图标识主观感受较差。   
不强依赖github的话，建议还是使用plantUML。

## PlantUML

PlantUML在github上只能使用外链，没法直接将markdown内嵌的plantuml代码渲染为图。  
但可使用PlantUML官网的Online Server存储UML，github中按引用图片的方式引用存储外链：  
拷贝server上的链接后，添加`https:`前缀，markdown中按`![](https:server URL)`方式引用。比如：
![sample](https://www.plantuml.com/plantuml/png/JP31QiCm44Jl-eeXvzhG74C8wQLGACcbnroszZfrK7UBTciQwCTNbcem23GQQJHFEffJyk_F6Bf8PZY_txXpxFUuid2YYCCXBEPlqpHuIedkhwDv2ABESFs23ajmXnV1ZIPw04-SxYZNNeH_dAKt-CTeKE7sFxrvcuqy24DKyb6kc3Ss8CFfSNseo3ntAfAhkB-8AuodWgcbtzeQt2xCRJilJjiirkJriS-gjI3ou3kS1Tbsz3oCmdr53-6OmVC7_G40)

同时，可以将引用的存储外链在Online server的解码为plantuml代码：  
从markdown内嵌的`![](https:Servel URL)`中拷出serverl URL，点击server网站的“Decode URL”按钮。  

本地使用时，推荐VScode中安装PlantUML插件。

## Mermaid

Mermaid已支持github上直接使用markdown内嵌，如：

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

## 综合比较

|项目|PlantUML|Mermaid|
|--|--|--|
|时间|||
|语法原理|DSL|DSL|
|版权|Github开源|Github开源|
|Github支持程度|引用外链|代码内嵌(较好)|
|Typora支持程度|未内置|内置(较好)|
|功能点|除标准UML外，还有架构图、json图等[文档5](较好)|基本的UML|

由于前几年支持了Github内置，目前github上Mermaid有49K星，而PlantUML仅6.4K星，前者将近是后者的10倍；commits数量，前者5K，后者不足1K，也将近5倍。   
对于常见的编辑器的支持，如typora、vnote也是内置支持的mermaid[文档5]，PlantUML需要额外配置支持。  
总结：
- 流行程度、软件支持情况上，Mermaid好于PlantUML；
- 制图丰富度上，PlantUML好于Mermaid；

## 参考文档
1. [PlantUML官网](https://plantuml.com/zh/)：PlantUML语法介绍及Online Server
2. [PlantText](https://www.planttext.com/)：UML在线绘制
3. [Mermaid在线绘图](https://mermaid-js.github.io/mermaid-live-editor/)
4. [Mermaid官网](https://mermaid-js.github.io/mermaid/#/)
5. [几种绘图语法的比较](https://gowa.club/Graphviz/%E5%87%A0%E7%A7%8D%E7%BB%98%E5%9B%BE%E8%AF%AD%E6%B3%95%E7%9A%84%E6%AF%94%E8%BE%83.html)

# Markdown内嵌(github)
</br>可内嵌HTML，但HTML表格内部（tr/td标签对中）无法再使用markdown解析；
</br>无法直接按语言段落内置plantuml或C语言，HUAWEI liteOS可以内置C语言的；可按链接方式链接plantUML server；
</br>无法显示同仓库下的图片：PC网络问题，代理网络可查看到图片。

# Git操作
- [git操作学习(动画版)](https://learngitbranching.js.org)
- [Git远程操作详解](https://www.ruanyifeng.com/blog/2014/06/git_remote.html)


