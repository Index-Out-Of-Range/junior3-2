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
    > 在状态处于活动状态期间，操作将继续运行。
    * Can be interrupted by other events.
    > 可能被其他事件打断。
    * If no event interrupt it, completion transitions will be issued
    > 如果没有事件中断，将发出完成转换
* Actions
    * Can be though of as being instantaneous
    > 可以是瞬间的
    * Can not be interrupted by other events. 
    > 不能被其他事件打断。

* Activities and completion transitions(活动和完成转换)
![](/images/2019年4月6日/2019-04-06_163457.png)
Activity：系统处于某个状态要做的事。
do/做完的时候出发complete，要执行completion transitions
而/后的叫做action，包括entry action和exit action都是原子的。
Activity不一样，activity会被中断，如按了stop则activity被无条件中断。
如果没有被中断，则执行完会执行completion trans

#### Internal transition: 
* Some events cause transitions to the current state, but without triggering the execution of the entry and exit actions.
> 有些事件会导致转换到当前状态，但不会触发进入和退出操作的执行。
* ![](/images/2019年4月6日/2019-04-06_163917.png)
> internal transition：状态里面要做一些动作
用户点击info，会出现一些时间等信息，但这时还是处于play状态。换句话说不会执行entry and exit action

## Composite states
> 复合状态 目的：使uml图更加简单，并不添加新的状态

* For complex systems, statecharts are often too complex for producing and understanding.
> 对于复杂的系统，状态集通常过于复杂，无法生成和理解。
* Composite states are used just for simplifying the statecharts.
> 复合状态仅用于简化状态集。
* Applicability: for states which have the common transitions (outgoing or incoming)
> 适用性:对于具有公共转换(传出或传入)的状态
* The states above are grouped together to form a composite state; the individual states are called substates.
> 将上述状态组合在一起形成复合状态;单独的状态称为子状态。

![](/images/2019年4月6日/2019-04-06_164322.png)
> 对于蓝色的，复合状态中的任何一个子状态都有这种跳转。
使得两个跳转变成一个跳转。
如果复合状态中有一个子状态是活动的，我们就说复合状态是活动的，且任何时刻只有一个子状态是活动的

#### Properties of composite states
* If a composite state is active, exactly one of its substate must also be active
> 如果一个复合状态是活动的，那么它的子状态中必须有一个也是活动的
* Outgoing transition: can flow from the composite state, or from a substate
> 传出转换:可以从复合状态流，也可以从子状态流
* Incoming transition: can flow to the composite state, or to a substate
> 传入转换:可以流到复合状态，也可以流到子状态
* Initial state: becomes active when an incoming transition reaches at the boundary
> 初始状态:当传入的转换到达边界时变为活动状态
* Final state: when ongoing activity has finished; issue completion transitions
> 最终状态:正在进行的活动结束时;问题完成转换
* Entry/exit actions

* 复合状态和普通状态一样，也会有他自己的初始状态和结束状态，如果有从外界到复合状态边缘，则会按照顺序。并且有entry action
![](/images/2019年4月6日/2019-04-06_164628.png)

## History states
> 最近从哪一次复合状态跳出的，就叫历史状态

* Requirement: if the “play” button is pressed, return to the CD player’s previous state, either “playing” or “paused”
* The composite state can remember a history state, denoted by an “H” state.
> 复合状态可以记住历史状态，用“H”表示。

![](/images/2019年4月6日/2019-04-06_164808.png)
> “play”转换的实际行为:
如果CD播放机正在播放，如果按下“播放”按钮，它应该从曲目开始播放，但是如果暂停，它应该一直暂停，直到再次按下暂停按钮。
要插入历史状态，只需双击“Busy”状态。
上面蓝色的指向H代表用户按下播放按钮,原来是play状态就转到play状态,原来是暂停状态就转到暂停状态。

![](/images/2019年4月6日/2019-04-06_165001.png)
> 如果历史状态是要激活的第一个状态，则应指定默认状态。
如果之前没有H,为空的时候,则用蓝线表明进入玩状态

![](/images/2019年4月6日/2019-04-06_165054.png)

## A “real” example
* Description of the automatic ticket machine
    * You select a type of ticket
    * The machine displays how much money you should continue to pay.
    * You insert coins
    * Two modes: “Change available” or  “Exact money required”
    * You have the option of entering money before selecting a ticket type
    * Cancel: press the “cancel” button or keep silence for 30 seconds

#### Preliminary statechart(初步的状态)
* A single (the most common) transaction
> 单个(最常见的)事务
* Every event leads to a transition between two states
> 每一个事件都导致两种状态之间的过渡
* It is unnecessary to name the states
![](/images/2019年4月6日/2019-04-06_165400.png)

#### Analysis of the preliminary statecharts
* The process can be divided into three stages:
    1. The machine waits for the user to select a ticket type;
    2. The user inserts coins into the machine;
    3. When the inserted coins is enough, the machine issues the ticket. Return to stage 1.

* Most stages correspond to states directly. But for the stages (e.g. stage 3) that only span short periods of duration, we can model them by actions.

![](/images/2019年4月6日/2019-04-06_165534.png)

* To model the alternative way:entering money before selecting a ticket type
    * Starting from the “idle” state, there is no transition labeled “coin”.
        => We need to create a new state

![](/images/2019年4月6日/2019-04-06_165718.png)

















