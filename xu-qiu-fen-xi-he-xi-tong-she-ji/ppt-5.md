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
> 建模另一种方法:在选择票证类型之前输入货币

    * Starting from the “idle” state, there is no transition labeled “coin”.
        => We need to create a new state
    > 从“空闲”状态开始，没有标记为“coin”的转换。=>我们需要创建一个新的状态

![](/images/2019年4月6日/2019-04-06_165718.png)

#### Integrating the transactions(整合转换)
* To model the sequence: 
    * Entering some coins ( but not enough)
    * Select a ticket type
    * Continue to enter coins
* We could create a new state. But eventually we find the new state is as the same as the existing one 
![](/images/2019年4月6日/2019-04-06_170812.png)

#### Time events
* Each state is supposed to contain an internal timer.
* The timer is reset every time the state is entered.
* The “after” event
* The “when” event
> after:经过某一时刻，会触发一个时间
when:指定某一时刻，会触发一个事件

![](/images/2019年4月6日/2019-04-06_170905.png)

## Action states
> 这一状态,不会响应任何事件,会有完成过渡

* Purpose of using action states: to avoid repetitions of transitions.
> 避免过渡的重复。
* An action state represents a period of time during which an object is performing some internal processing
> 动作状态表示对象执行某些内部处理的一段时间
* It only contains an activity
* It can not respond to external events.The transitions leaving an action state can only be completion transitions.
> 它不能响应外部事件。离开操作状态的转换只能是完成转换。
* Do not overuse them.

> 教科书在这里有一个错误:它错误地将“行动状态”(Action States)称为“活动状态”(Activity states)。
两者的区别是:
动作状态(Action state):不能被外部事件中断。
活动状态(Activity states):可以被外部事件中断。它有更复杂的语义。

* Without action states, some transitions must be repeated.
![](/images/2019年4月6日/2019-04-06_171401.png)

* With action states, we get a clearer figure.
![](/images/2019年4月6日/2019-04-06_171448.png)

#### The complete statechart for the ticket machine
![](/images/2019年4月6日/2019-04-06_171521.png)

## Question
#### Q1:
* Suppose that the ticket selection buttons are deactivated once a ticket type has been selected, and only reactivated at the end of a transaction.
> 假设一旦选择了票券类型，票券选择按钮就被禁用，并且只在事务结束时重新激活。

#### A1:
* In  Idle or No ticket selected  state, a single press of the ticket type button leads to transitions ending at the ticket selected state. Thus, we need only to study the last state.
> 在空闲状态或没有选择票证的状态下，只需按一下票证类型按钮，就可以在票证选择状态结束转换。因此，我们只需要研究最后一种状态。
* Add an entry action to deactivate the buttons
> 添加一个条目操作来禁用按钮
* Since all transitions leaving from the ticket selected state end at the Idle state, we can add an exit action into the state to reactivate the buttons.
> 由于所有离开票选状态的转换都以空闲状态结束，所以我们可以在状态中添加一个exit操作来重新激活按钮。

![](/images/2019年4月6日/2019-04-06_172141.png)

#### Q2:
* Suppose that once enough money has been entered to pay for the required ticket, the coin entry slot is closed, and only reopened once any ticket and change has been issued.
> 假设已经输入了足够的钱来支付所需的票款，那么硬币进入槽就关闭了，只有在发出任何票款和更改之后才重新打开。

#### A2:
* In  Idle or No ticket selected  state, the machine does not know what type of ticket is required by the user, so it is impossible to judge whether the entered money is enough. Thus, the slot is kept open.
> 在Idle或No ticket selected状态下，机器不知道用户需要哪种类型的票，所以无法判断输入的钱是否足够。因此，插槽保持打开状态。
* In the ticket selected state, when enough money has been entered, the machine jumps into the action state. 
> 在票选状态下，当输入足够的钱时，机器就跳转到动作状态。
* Thus, we add an entry action into the action state to close the slot.
> 因此，我们在操作状态中添加一个条目操作来关闭插槽。
* Since the slot is reopened only after the ticket and change is issued, we add an entry action into the idle state.
> 由于插槽仅在票证和更改发出后才重新打开，所以我们将一个entry操作添加到空闲状态。

![](/images/2019年4月6日/2019-04-06_172323.png)

## Implementation of statecharts
* Solution 1
    * The states are modeled by an enumeration variable.
    > 状态由枚举变量建模。
    * “Switch” statements are used for the member functions whose behaviors varies with the state.
    > “Switch”语句用于行为随状态变化的成员函数。
* Drawbacks(缺点)
    * When a new state is added, all functions should be changed.
    * Some functions contain many empty cases in the switch statement

* Solution 2:
    * Suppose class A has n states. Each state is modeled by a state class.
    > 假设A类有n种状态。每个状态都由一个状态类建模。
    * All the state classes are generalized to a root class.
    > 所有状态类都被概括为一个根类。
    * Class A holds a pointer (to the root class).
    > 类A持有一个指针(指向根类)。
    * For incoming messages, class A simply pass them on to the object representing the current state.
    > 对于传入消息，类A只是将它们传递给表示当前状态的对象。
    * The root class has an interface to process all messages sent to class A.
    > 根类有一个接口来处理发送到类A的所有消息。
    * Each state class only re-define functions for the messages that interest it.
    > 每个状态类只为它感兴趣的消息重新定义函数。
    * Each state is capable of destroying itself, creating a new object representing a new state, and setting the current state to the new state.
    => bidirectional association between class A and the root class is necessary.


![](/images/2019年4月6日/2019-04-06_172451.png)



```
class CToolState {
	virtual void Press()=0;
};
class CreationTool{
    CToolState* state;
	void Press() {state->Press();}
}
```


> 每个状态对应一个类
任意时刻只有一个类是活跃的
Creation的指针指向唯一活跃状态，事件转发给活跃状态。
活动状态会再次转发给活动对象

> 状态跳转如locatingStart跳转到LoacatingStop
鼠标按下的事件处理函数在locatingStart函数，但他自身不可能修改指针。他只知道要切换状态了，所以要切换状态时不能让状态的子类去执行操作。
所以要把转换状态的任务上升到基类。CToolState也执行不了，再次回传给CreationTool，他可以做












