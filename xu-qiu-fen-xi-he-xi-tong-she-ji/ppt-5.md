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

