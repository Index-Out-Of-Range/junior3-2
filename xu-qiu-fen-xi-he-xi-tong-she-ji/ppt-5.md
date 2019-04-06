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
* Interaction diagram Vs. statecharts
    * The former: a short period, a single user generated transaction, a certain sequence of messages
    * The later: an object’s whole life, all possible messages it can accept.
* How to construct states
    * An object in a particular state will respond differently to at least one event from the way in which it responds to that event in other states.
* (Active) state, event (triggers) and transitions

