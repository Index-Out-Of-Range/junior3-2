## Class diagram
* An example: how to draw a class diagram
* Operations
* Associations,  association generalization
* Aggregation（聚合）
* Composite objects
* Association classes
* Qualified associations
* Multiple inheritance in UML
* Mixin class

#### Classes and associations
* There is direct correspondence between class associations and object links.
> 类关联和对象链接之间存在直接对应关系。
* Multiplicity: Demo（多重性的一个演示）
![](/images/2019年4月5日16点32分.png)
> Rectangle Tool是用来创建Rectangle比如左上角和右上角的坐标。要么为0要么为1。一个Demo只能有一个RT，一个RT只能隶属一个Diagram，即多个Diagram不能共享一个RT

#### Multiple associations
* ![](/images/2019年4月5日16点42分.png)
> 两个类可以有多个关联关系
一个Editor能打开多个Diagram进行编辑所以是1对n
任何时刻只能看到一个框图，起名为current。
0..1其中1意思是给定一个Editor只能有一个Diag,1个Diag只能对应一个Editor 0是指；

#### Class Generalization
* ![](/images/2019年4月5日16点45分.png)
* Direct implementation would lead to redundant Vectors
> 直接实现会导致冗余向量
* 只要一些类有共同的属性，则应该设计一个基类。

#### A more reasonable design
* ![](/images/2019年4月5日16点47分.png)
* Does not introduce new relationship between objects
> 不引入对象之间的新关系
> 抽象出基类

#### Similar for Creation Tools
* ![](/images/2019年4月5日16点49分.png)

#### The instantiate relationship
* Consider the relationship between RectangleTool and Rectangle
* The associate relationship is not applicable, since the connection is not permanent
> 关联关系不适用，因为连接不是永久性的
* The instantiate relationship
![](/images/2019年4月5日16点52分.png)

> Instantiate 实例化：C++中多种场合用到：1. 实例化对象 2.给定模板参数实例化类 3.给定一个函数模板及参数，实例化出函数
> UML中也有**实例化** 双尖括号左边的类的对象，能创建右边类的对象

#### Attributes and Operations
* ![](/images/2019年4月5日16点54分.png)
* Variable number of data elements.
> 可变数量的数据元素。
* Format of operations.

* UML**抽象类**用**斜体**表示
* 一个分割后是该类的数据成员，左边的锁表示protect或private，*号代表若干个元素组成，这个元素类型是point
* 之后是成员函数。
* Tips：
    * 绘制UML是设计阶段的事情,没有必要把所有数据成员和成员函数列全，这属于编码阶段的考虑
    * 在设计之初可以不罗列出数据成员，先列出主要的成员函数

![](/images/2019年4月5日17点00分.png)
* Selected是角色role，离Element较近
* Resizing位于正中间则不是角色

#### Multiplicity（多重性）
* Definition: the number of times a given entity can occur in some context.
> 定义：给定实体在某些上下文中可以出现的次数。
* Notation: number ranages
    * E.g., 0..9
    * \* => infinity
    * Abbreviation, e.g., 1..1 => 1
    * Could be a list, e.g., 0, 3..*

#### Class multiplicity（类多重性）
* Definition: the number of instances of the class that can exist.
> 可以存在的类的实例数。

    * The relationship of “instance of” is rarely shown.
    > 很少显示“实例”的关系。
* Default: 0..*
> 默认值
* Notation for singleton class

* ![](/images/2019年4月5日17点12分.png)
> 类的右上角有数字比如1，则表示单一模式，只能有一个对象。

#### Attributes of classes（类的属性）
* Attributes format
    * In the early stages: `name`
    * Common format:   `name: type`
    * Complete format: `name: type = default_value`
* Other classes should not be used as the attribute types => association
> 其他类不应该用作属性类型
* Instance scope
> 实例范围
* Class scope: underlined
> 类范围：下划线
* Multiplicity of attributes
> 多种属性

* ![](/images/2019年4月5日17点16分.png)
> 静态成员或成员函数用下划线表示

#### Operations of classes
* Format:
    * name(p:parameter_type,…): return_type
    * The types are **optional**
* Instance scope and class scope
* ![](/images/2019年4月5日17点19分.png)

#### Object identity
* It is an intrinsic feature of objects
* Even two objects have the same set of values for all attributes, they have two different identity
* It is different from the identifying attribute of a class
* ![](/images/2019年4月5日17点21分.png)












