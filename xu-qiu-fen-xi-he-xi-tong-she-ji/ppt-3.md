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
> 公共祖先(如果有)的属性和操作只继承一次

* An example of multiple inheritance
![](/images/2019年4月6日/2019-04-06_143422.png)
> Possible name clash: “date” of document and message
可能的名称冲突:文档和消息的“日期”

* Multiple inheritance with a common ancestor
![](/images/2019年4月6日/2019-04-06_143534.png)

#### Mixin class
* A mixin class: is intended to provide an optional interface or functionality to other classes. The functionality should be independent with that of the existing classes.
> 旨在为其他类提供可选的接口或功能。功能应该独立于现有类的功能。
* It is similar to an abstract classes in that it’s not intended to be instantiated. 
> 它类似于抽象类，因为它不打算实例化
* Mixin classes require multiple inheritance.
> Mixin类需要多重继承。

* Illustration of mixin classes
![](/images/2019年4月6日/2019-04-06_143802.png)
> Mixin class 是附加类。当需要这些功能时，继承该类即可。

* If without mixin class
![](/images/2019年4月6日/2019-04-06_144134.png)

* With Mixin class
![](/images/2019年4月6日/2019-04-06_144513.png)
> Acount是基本类
Chequebook作为附加功能

* Discriminators（鉴别器）
![](/images/2019年4月6日/2019-04-06_144755.png)
> Discriminator即为分类的标准

## Implementing associations
* Uni-directional links
    * simple to implement
    > 易于实现
    * Will lead to problems if they are later modified to bi-directional links
    > 如果以后修改为双向链接会导致问题吗
* Bi-directional links
    * Complex to implement => consistency
    > 实现复杂
    * With no risk
* Both styles of implementation should be hidden from client code
> 这两种实现风格都应该对客户机代码隐藏
> Uni-directional: 单一方向可抵达性 通过A到达B，不能从B到A
Bi- xxx: 互相。。强调一致性
单向的简单，但是不利于软件的演化；**双向的维护一致性较为麻烦**

#### Uni-directional implementations
* The multiplicity at the tail of the arrow has no effect on the implementation
> 箭头尾部的多重性对实现没有影响
* Mutable and immutable associations
> 可变和不可变关联
* To implement the semantic(语义的) correctly, we need:
    * Proper declarations of data members, *and*
    * Proper definitions of member functions
    
* ![](/images/2019年4月6日/2019-04-06_150213.png)
> 讨论mutable和immutable时一定要考虑方向



* ![](/images/2019年4月6日/2019-04-06_150628.png)
```
#include <iostream>
#include <vector>
using namespace std;
class B {
	//...
public:
	operator ==( B & r) {};
};
class A {
    vector<B> links;
public:
    addLink(B & b) {
		links.push_back( b );
	};
    removeLink(B & b ){
        vector<B>::iterator it;
        for ( it=links.begin(); it!=links.end(); it++) {
            if ( *it == b) break;
        }
        if ( it != links.end() )
            links.erase(it);
    };
}
main()
{
}
```

#### Bidirectional implementation
![](/images/2019年4月6日/2019-04-06_150806.png)
> 拥有一个account的时候可以申请可以不申请debitcard
拥有Debitcard一定对应一个account
Mutable的含义：在account的生存期之间，可以对应多个debitcard但同一时间最多一个



```
class DebitCard;
class Account {
	DebitCard * card;
public:
	DebitCard& getCard() {}
    void setCard(DebitCard & p_card ) {}
    void removeCard() {}
};
class DebitCard{
	Account * theAccount;
public:
	DebitCard(Account & a) {}
	getAccount(){} 
}
main() 
{
	Account a1;
	Account a2;
	DebitCard card1(a1);
	a1.setCard(card1); 
	//a2.setCard(card1);  cause problem!
}
```
* A better solution



```
class Account;
class DebitCard{
	Account * theAccount;
private:
	DebitCard(Account & a) {}
public:	
	getAccount(){} 
	friend class Account;
};
class Account {
	DebitCard * card;
public:
    void addCard() {
		card = new DebitCard(*this);
	}
    DebitCard& getCard() {}
    void removeCard() {}
};
main() 
{
	Account a1;
	a1.addCard();
}
```
> 只给其中一个类指定维护关联的责任。
类DebitCard的“private”和“friend”:确保只有Account类可以创建指向对象的链接
类DebitCard。
所有的创建都在一个成员函数中完成;

#### Bidirectional implementation: both directions are immutable(不可变的)
* A typical mistake: want to create the link within a single step.
![](/images/2019年4月6日/2019-04-06_151523.png)



```
#include <iostream>
using namespace std;
class Guarantor;
class Account {
  public:
	Guarantor * pGuarantor;	  
	int i;
	Account( Guarantor * g) {
		pGuarantor = g;
		i = 100;	
              f();
	}
	virtual f()  {cout << "f\n"; }
};
class Guarantor {
public: Account * pAccount;  
    int j;
    Guarantor(Account * a){
		  pAccount = a;   j = 200;
		  g();		  
		  //a->f();
		  //cout << a->i;
	}
	virtual g(){ cout << "g\n"; }
};
main ()
{  
    Account *a = new Account(new Guarantor(a) ); 
    cout << a->pGuarantor->j;
    //cout << a->pGuarantor->pAccount->i;
}

```

























