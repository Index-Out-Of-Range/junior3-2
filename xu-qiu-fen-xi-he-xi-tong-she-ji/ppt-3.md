## Overview of last course
* Chapter 6 Class diagram
    * Operations
    * Associations,  association generalization
    * Aggregation
    * Composite objects
    * Association classes
    
## Outline of this course
* Class Diagram
    * Qualified associations
    * Multiple inheritance in UML
    * Mixin class
    * Discriminators
* Implementation of class diagram
    * Uni-directional association
    * Bi-directional association
    * Implementing qualifiers
    * Implementation of association classes
    
> Qualified associations: 利用关键字标记对象
Multiple inheritance: 特殊的继承：多继承  
Mixin使用多继承实现设计的目标：有一个完成基本功能的基类，有多个Mixin类实现一个附属的功能
Mixin class：即表示多继承关系，同时一种设计模式

#### Qualified associations（修饰关联）
* An example: Unix file system
    * Each file has a unique internal identifier（内部标识符）
    * Each file can appear multiple times in different directories, even including in the same directory.
    * All names within a directory must be different from each other.

* Informal illustration of qualified association（修饰关联的非正式例证）
![](/images/2019年4月6日/2019-04-06_140840.png)
> Linux 允许同一个目录下不同名字指向同一个文件

* Association class can not describe the relationship
![](/images/2019年4月6日/2019-04-06_141137.png)
> Reasons: It does not allow: a directory may havedifferent names linked to the same file
没法描述一个目录下不同的文件名指向同一个文件。因为同一关联只能发生一次不能发生多次。因此引入qualified associations，会频繁使用

* **Definition**: an association class which has properties which enable it to act as a key
> 一个association class，它具有使其能够充当键的属性
* Mapping from qualifier values to instances of the class at the other end of the association
> 从限定符值映射到关联另一端的类的实例
![](/images/2019年4月6日/2019-04-06_141810.png)
> 0对应的是给定的name不存在该目录下。
给定一个存在的名字，能对应到一个file
文件名相当于关键字的作用

#### Qualifiers and identifiers(限定符和标识符)
* Use of an attribute as an identifier
![](/images/2019年4月6日/2019-04-06_143001.png)
* Better: Use of a qualifier
![](/images/2019年4月6日/2019-04-06_143012.png)

#### Multiple inheritance in UML（UML中的多继承）
* UML allows multiple inheritance
* Attributes and operations of the common ancestor (if any) are inherited only once



















