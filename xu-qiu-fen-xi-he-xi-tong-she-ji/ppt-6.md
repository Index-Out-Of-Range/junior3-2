## Outline
* Introduction
    * Description of a pattern
    * Features of the book, notations 
    * Roles of design pattern
* A case study: designing a document editor
    * Composite pattern (document data)
    * Strategy pattern (document formatting)
    * Decorator pattern (interface elements)

* The concept of design pattern
> “Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice”
每个模式都描述了一个在我们的环境中反复出现的问题，然后描述了这个问题的解决方案的核心，这样你就可以将这个解决方案反复使用一百万次，而不用重复做同样的事情。

* 使得代码更通用：设计模式目标之一
![](/images/2019年4月6日/2019-04-06_192345.png)



```
#include <iostream>
#include <vector>
#include <list>
#include <math.h>
using namespace std;

template <class Container>
void Display_Container(Container c)
{
	Container::iterator it;
	for (it=c.begin(); it!=c.end(); it++)
		cout << *it << " ";
	cout << endl;
}
template <class Container>
void Sort(Container & c)
{	Container::iterator it1, it2;
	Container::value_type  temp;
		
	for (it1=c.begin(); it1!=c.end(); it1++) {
		for (it2=it1; it2!=c.end(); it2++) {
			if ( *it1 > *it2 ) {
				temp = *it1;
				*it1 = *it2;
				*it2 = temp;			
			}
		}	    
	}
}
int main()
{  
	vector <int> v;   
	list <double> l;   

	for (int i=10; i>=0; i--) {
		v.push_back(i);
		l.push_back( sin(i*3.14) );
	}
	Display_Container(v);    
	Display_Container(l);  
	Sort( v );     
	Sort( l );
	Display_Container(v);    
	Display_Container(l);  
	return 0;
}
```

#### Description of a pattern
* Pattern name (singleton)
* The problem
	* Not the basic data structures, nor the entire system
	> 不是基本的数据结构，也不是整个系统
	* Not domain specific
* The solution
* The consequence ( discussion)
	* Space and time trade-offs
	* Language and implementation issues
	* Impact on a system’s  flexibility, extensibility, and portability.
	
#### Roles design patterns play
* Application programs
	* Use design patterns to reduce the class dependencies, platform dependencies, etc.
* Toolkit
	* Use design pattern for code reuse
	* For example: containers, iterators and algorithms in C++ STL.
* Frameworks
	* Emphasize design reuse
	* Use of patterns in a framework makes learning the usage of the framework easier










