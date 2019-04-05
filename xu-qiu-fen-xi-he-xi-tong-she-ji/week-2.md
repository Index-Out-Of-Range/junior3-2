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



