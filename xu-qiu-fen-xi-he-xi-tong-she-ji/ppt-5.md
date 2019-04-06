## Outline
* Why statecharts
* State,transition, Initial and final states
> 状态，过渡，初始和最终状态
* Actions, guard conditions
* Entry and exit actions
* Activities
* Composite states
* History states
* A “real” example
* Quiz on the automatic ticket machine
* Implementation of statecharts

> Sequence不能完全描述系统对时间的处理，关注的短时间的很局部的处理，并没强调长时间的响应。

## Why Statecharts
* Interaction diagram Vs. statecharts(交互图与状态图)
    * The former: a short period, a single user generated transaction, a certain sequence of messages
    > 前者:短时间内，单个用户生成事务，消息序列一定
    * The later: an object’s whole life, all possible messages it can accept.
    > 后者:一个对象的整个生命周期，它可以接受的所有可能的消息。
* How to construct states
    * An object in a particular state will respond differently to at least one event from the way in which it responds to that event in other states.
    > 处于特定状态的对象对至少一个事件的响应与它在其他状态中对该事件的响应方式不同。
* (Active) state, event (triggers) and transitions
> (活动)状态、事件(触发)和转换

#### Components of a statechart
* State
* Event
* Transition(过渡；转变)
* Initial and final states
* Actions 

* The CD player example
![](/images/2019年4月6日/2019-04-06_161923.png)
> 不同的按钮在不同的状态下有不同的功能。

## Guard conditions and actions
* Guard condition: 当某个条件被满足的时候，才会发生跳转。中括号。
如在closed中按play在【no cd】和【cd present】条件下跳转的状态是不同的
![](/images/2019年4月6日/2019-04-06_162140.png)

## Entry and exit actions
* Entry actions are performed every time a state becomes active, immediately after actions on transitions leading to the state have completed.
> 每次状态变为活动状态时，都会立即执行条目操作，这是在导致状态的转换操作完成之后执行的。
Entry action：进入这个状态的准备工作。目的：指导我们在编码阶段要实现


* Exit actions: are performed whenever a transition is fired to leave the state.
> 退出操作:在触发转换以离开状态时执行。

* Entry and exit actions. Applicable for self-transitions too.(也适用于自我转换。)
![](/images/2019年4月6日/2019-04-06_163202.png)

## Activities
* Activities
    * The operation continues to run throughout the period when the state is active.
    * Can be interrupted by other events.
    * If no event interrupt it, completion transitions will be issued
* Actions
    * Can be though of as being instantaneous
    * Can not be interrupted by other events. 
















