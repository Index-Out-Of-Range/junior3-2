## Outline
* Use-case Diagram
    * Actors
    * A use-case should be abstract
    * Generalization,Specialization
    * Inclusion, Extension
* Sequence Diagram
    * First step of designing(设计的第一步)
    * An example
    * Components of a sequence diagram
    * Collaboration diagram
    * Conditional/asynchronous message,etc

## Introduction to Use-case Diagram
* Role played(作用)
    * Initial statement of the requirements.（需求的初始陈述。）
    * As detailed as you can.
    * External visible behavior of the system.（系统的外部可见行为）
* Components
    * Actors: the roles that users can play
    * Use case: the interaction between actors and the system
    
> 用例：要实现某个功能的总体性的描述，针对最终结果即可，如保存文档。不用考虑途径和异常

#### Actors
* Usually: different groups of users
* No one-to-one correspondence between a single user and an actor
> 单个用户和参与者之间没有一对一的通信
* Not necessarily be human 
    * Human
    * Computer systems
    * Some devices

#### Use case
* Should be **abstract**
    * Not every piece of operation can be viewed as a use case
    * Exceptions can NOT be viewed as separate use cases.
* **Definition**:a description of a whole class of interactions that have the same overall intention. 
> 对具有相同总体意图的整个交互类的描述。
* Consists of
    * A basic course of events
    * Alternative courses
    * Exceptional courses
* The use case diagram of the diagram editor example
![](/images/2019年4月6日/2019-04-06_153912.png)

#### Generalization and Specialization
* Abstract use case, Explanation for a use case
![](/images/2019年4月6日/2019-04-06_153954.png)

#### Inclusion of use case(包含用例)
* Stereotype: specification of a relationship
> 原型:关系的规范

![](/images/2019年4月6日/2019-04-06_154115.png)
> 先要实现右边的才能实现左边的

#### Realization of a use case
* Describe how a set of objects can interact with each other to implement the use case.
> 描述一组对象如何相互交互以实现用例。

    * For designer: to build up an understanding of the objects, classes and interactions
    > 对于设计人员:建立对对象、类和交互的理解
    * The first step of design
    * Do not consider the GUI elements
* Notation: interaction diagrams(符号:交互图)
    * Sequence diagrams (more informative)
    * collaboration diagrams (more concise(简洁的))

> 用例图丝毫不考虑软件是怎么设计，只考虑需求
Sequence图是软件设计迈出的第一步：为了实现这个用例，应该有哪些对象，这些对象应该怎样协同工作去实现用例

* Realization of the “create diagram” use case
    * Multiple diagrams 
        => We need a “diagram” class
    * Only one active diagrams
        => We need a “DiagramEditor” object
    * The “DiagramEditor” should have a link 
![](/images/2019年4月6日/2019-04-06_154549.png)

* A sequence diagram
![](/images/2019年4月6日/2019-04-06_154643.png)
* 比较复杂的才绘制sequence图，尤其是多线程
* Elements in a sequence diagram
    * Objects are shown at the top.
    > 对象显示在顶部
    * Time flows downward.
    > 时间线向下流动
    * Lifeline.
    * Messages & message to oneself
    * Activation: processing a message.
    > 激活:处理消息。
    * Construction of a new object.
    > 构造一个新对象

* Creating a rectangle element 
![](/images/2019年4月6日/2019-04-06_155157.png)
> 序列图不反映演示程序的实际序列。但是这并不重要，因为我们的目标只是比较两种类型交互图之间的差异。

* A collaboration diagram
![](/images/2019年4月6日/2019-04-06_155255.png)
> Order of the messages should be explicitly specified.
应该显式指定消息的顺序。

* 这个序列图显示了选择一个元素的过程。
![](/images/2019年4月6日/2019-04-06_155424.png)

* Deleting an element: Termination of objects
![](/images/2019年4月6日/2019-04-06_155801.png)

* Moving an element: use case extension
![](/images/2019年4月6日/2019-04-06_155853.png)

* Hierarchical numbering of messages(消息的分级编号)
![](/images/2019年4月6日/2019-04-06_155956.png)
> Can also be used in collaboration diagram
当然，对于简单的序列图，没有必要进行编号。


























