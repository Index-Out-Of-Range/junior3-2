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

#### Object identity(对象标识)
* It is an intrinsic feature of objects
> 它是物体的固有特征
* Even two objects have the same set of values for all attributes, they have two different identity
> 即使两个对象对所有属性具有相同的值集，它们也具有两个不同的标识
* It is different from the identifying attribute of a class
> 它与类的标识属性不同
* ![](/images/2019年4月5日17点21分.png)

#### Associations
* Associations, role names, multiplicity
* ![](/images/2019年4月5日17点38分.png)
>Worksfor是Associations的名字
Employee和employer是角色
* Self-associations
* ![](/images/2019年4月5日17点38分（1）.png)

#### Links do not have identity
The problem: John is employed as a lecture and a bar attendant by a company
> 问题是：约翰被聘为公司的讲座和酒吧服务员

* An illegal diagram in UML
* ![](/images/2019年4月5日17点40分.png)

* Possible solution
![](/images/2019年4月5日17点42分.png)

#### Generalization and specialization(泛化和特殊化)
* Superclasses (ancestors), subclasses (descendants), generalization, specialization,abstract classes, inheritance, overriding operations in subclasses
> 超类（祖先），子类（后代），泛化，特化，抽象类，继承，子类中的重写操作
* Abstract operations (pure virtual functions)
> 抽象操作（纯虚函数）
* ![](/images/2019年4月5日17点44分.png)

#### Association Generalization
* An example: a customer can hold at most one Current Account.
* ![](/images/2019年4月5日17点51分.png)
> If without the generalization: (1) two associations have the same name. (2) There are two paths from the Customer class to the CurrentAccount class. Thus, a customer may holds two current accounts, according to the diagram.
> 绿线是联系之间的限制条件，只能由下面的到达curentAccount

#### Aggregation
* Is just a kind of association
    * Most often it is used to describe part/whole relationship.
* Properties when objects are linked to instances of their own class.
> 对象链接到其自己的类的实例时的属性。

    * Anti-symmetry: no self-connection
    > 反对称：没有自我连接
    Anti-symmetry:反自身 一个对象不能和自己发生Aggregation’
    * Transitivity: if A is a part of B, and B is a part of C, then A is also a part of C.
    > 传递性：如果A是B的一部分，而B是C的一部分，那么A也是C的一部分。
* A “normal” aggregation relationship
* ![](/images/2019年4月5日17点55分.png)
> Put a diamond in the “whole” end.
> 菱形代表母体

* If without aggregation
* ![](/images/2019年4月5日17点56分.png)

* …leading to meaningless object diagrams
* ![](/images/2019-04-05_175644.png)
> Cyclical object structures
> 循环对象结构

* Solve the problem with aggregation
![](/images/2019-04-05_175750.png)
> The two cyclical structures can be ruled out
> 可以排除上面的两种循环结构
> 解决了上一张的两个问题
不能self-
由于传递性 y->z->y，不能self-

* Aggregation: not necessarily be part/whole relationship
![](/images/2019-04-05_180021.png)

## Composite objects
* Composite: a strong form of association
    * A “part” can only belong to one composite object
    > 部分”只能属于一个复合对象
    * When a composite object is destroyed, all its dependent parts must be destroyed at the same time
    > 当复合对象被销毁时，必须同时销毁其所有相关部分
    * UML notation: solid diamonds
    > UML表示法：实心菱形

* An example of composition
![](/images/2019-04-05_180414.png)
> 当删除一个MailMessage时，Attachment并没有被删掉。
实心空心






