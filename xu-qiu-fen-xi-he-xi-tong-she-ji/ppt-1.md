## 难点
### Views
* Use Case View
* Design View
* Implementation View
* Process View
* Deployment View

# Chapter 1

## Model
#### Definition: 
* the intermediate descriptions (documents) produced in the process.
> 过程中产生的中间描述（文件）。

#### Features: 
* Abstract view of a system.
* Easy to understand.
* A valuable means for communication.

#### Relationship between analysis models and design models
* analysis models → design models
* What if different languages are used for the two phases?
> Information can not be accurately translated.
* **OO technology**: use the same kinds of models in the two phases.
    * The analysis models will be preserved and recognized in the design phase.
    > 分析模型将在设计阶段得到保留和认可。
    * Design phase: just adding some details.Thus, the course only covers the design phase.
    > 设计阶段：只需添加一些细节。 因此，该课程仅涵盖设计阶段。

## Methodologies(方法)
![](/images/2019年3月23日21点59分.png)

#### Classes of methodologies
* Structured methods
    * Models: a collection of data +functions external to the data
    * Notations: data flow diagrams
    > 符号：数据流图
* Object-oriented methods
    * Models: to be covered in Chapter 2
    * Notations
    > Unified Modeling Language (UML)
    
#### A brief Introduction to UML
* The dominant language in OO modeling
> 面向对象建模中的主导语言
* It can be used with a wide range of software processes
* **Views**
![](/images/2019年3月23日22点07分.png)
![](/images/2019年3月25日21点40分.png)
![](/images/2019年3月25日21点41分.png)
![](/images/2019年3月25日21点42分.png)
* Models
    * Model elements
* Diagrams
    * A diagram presents certain aspect of the underlying system model.Diagrams are just like programs, but more abstract (object structure).
    > 图表显示了底层系统模型的某些方面。 图表就像程序一样，但更抽象（对象结构）。
    * Some types of diagrams can be used in both use case and design views
    > 某些类型的图表可以在用例和设计视图中使用
    * UML’s diagram types
    | Diagram                 | View                   |
    | ----------------------- | ---------------------- |
    | 1 Use case diagram      | Use case view          |
    | 2 Object diagram        | Use case & design view |
    | 3 Sequence diagram      | Use case & design view |
    | 4 Collaboration diagram | Use case & design view |
    | 5 Class diagram         | Design view            |
    | 6 Statechart diagram    | Design view            |
    | 7 Activity diagram      | Design view            |
    | 8 Component diagram     | Implementation view    |
    | 9 Deployment diagram    | Deployment view        |
    
#### The software development process
* Linear or waterfall model
    * Analysis -> Designing -> Development -> Testing -> Deployment
* Iterative model
    * ![](/assets/2019年3月25日21点58分.png)

---
# Chapter 2

## Modeling with objects
* The object model
    * Data + Operations
    * Execution of a program: a dynamic network of intercommunicating objects.Nodes (object) + links (sending messages)
    > 程序的执行：相互通信对象的动态网络。 节点（对象）+链接（发送消息）
    * The semantic foundation for UML’s design models
    > UML设计模型的语义基础
* The stock control example
    * Name,catalogue,cost
* Design: how to split up a system’s data and overall functionality.
> 设计：如何分割系统的数据和整体功能。
* A frequently used rule: **real-world objects**
* Class

    ![](/images/2019年4月5日14点25分.png)
    
#### Object Properties（对象属性）
* State: the aggregate of the data values contained in an object’s attributes
> 对象属性中包含的数据值的聚合
* Behavior: shown in the class diagram
* Identity: address in memory
> 身份：内存中的地址
* Object names: a convenient alias for its identity.
> 对象名称：其标识的方便别名。

#### Avoiding data replication（避免对象复制）
* Data in the previous object model is replicated
    * Waste storage
    * Difficult to consistently update all objects
* Links
    * ![](/images/2019年4月5日14点31分.png)



```
#include <iostream>
using namespace std;
class CatalogueEntry {
public:
	CatalogueEntry(string p_name, long p_number, double p_cost){
		name   = p_name  ;
	    number = p_number;
		cost   = p_cost  ;
	}
	string getName()   { return name;};
	long   getNumber() { return number; };
	double getCost()   { return cost;};
private:
	string name;
	long number;
	double cost;
};

class Part{
public:
	Part(CatalogueEntry * e){
		entry = e;
	}
private:
	CatalogueEntry * entry;
}
main()
{
	CatalogueEntry *screw = new   
         CatalogueEntry("screw",28834,0.02);
	Part * screw1 = new Part(screw);
}
```

#### Navigability（导航性）
* ![](/images/2019年4月5日14点36分.png)

#### Message Passing
* ![](/images/2019年4月5日14点39分.png)

#### A simple structure
* ![](/images/2019年4月5日14点40分.png)

#### A more realistic structure
* Impossible for implementation!
* ![](/images/2019年4月5日14点41分.png)

#### Use of abstract class
* ![](/images/2019年4月5日16点13分.png)

#### Object diagram
* ![](/images/2019年4月5日14点44分.png)

#### Late Binding & Polymorphism（多态性）
* ![](/images/2019年4月5日14点45分.png)

## Class Diagrams（类图）
* Object diagrams: can only show a small subset of a program’s possible states.
> 只能显示程序可能状态的一小部分。
* We need to describe the software system in a more abstract level: class diagrams.
> 需要在更抽象的层面上描述软件系统
    * Similar to object diagram
    * Types of the attributes are shown（显示属性的类型）
    * Association (linkage counter)
    * Inheritance（继承）
    
#### An example of class diagram
* ![](/images/2019年4月5日14点48分.png)

#### The applicability of the object model（对象模型的适用性）
* Often: object (real world) => object model
* Exceptions: the example above
* Message passing: no direct association(消息传递：没有直接关联)
    * Example: people bump
    * Objects + events => Objects + messages
* Strength of OO
    * Localization of data and operations
    > 数据和操作的本地化
* In most cases, the following mapping holds(在大多数情况下，以下映射成立)
    * real world object => object model
    > 真实世界对象 => 对象模型



