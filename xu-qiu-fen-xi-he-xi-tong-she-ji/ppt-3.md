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


























