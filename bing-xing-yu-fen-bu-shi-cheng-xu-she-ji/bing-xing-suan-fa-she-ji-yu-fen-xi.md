## 并行算法设计

## 并行算法分析

### 基本指标

* 串行算法评价：算法时间复杂度表示为输入规模的函数
* 并行算法评价：除了输入规模之外，还应考虑处理器数目、处理器相对运算速度、通信速度

#### 评价标准

* 运行时间
* 加速比：并行算法比串行算法快多少？
  * 很多串行算法，选哪一个？

#### 并行程序设计的复杂性

* 足够的并发度（Amdahl定律）
* 并发力度
  * 独立的计算任务的大小
* 局部性
  * 对临近的数据进行计算
* 负载均衡
  * 处理器的工作量相近
* 协调和同步
  * 谁负责？处理频率

#### 并行算法额外开销

#### cache引起的超线性加速

* 2个处理器的并行系统，问题规模W
* 每个处理器由cache 64KB，命中率80%，cache延迟2ns，DRAM100ns，平均访问时间

> 2 \* 0.8 + 100 \* 0.2 = 21.6 ns

* 若
* 
#### 搜索分解导致超线性

### 可扩展性

#### 效率

* 理想并行算法，S=p
* 难实现，不是100%的时间都用于有效计算
* 求和例子，部分时间处理器处于空闲
* 效率：度量有效计算时间

#### 代价

* 并行算法运行时间 \* 处理器数量
* 所有处理器用来求解问题的时间总和
* E = Ts/cost,
  * p = 1时，cost = Ts
* 代价最优：代价与最优串行算法运行时间渐进相等——E= θ\(1\)

#### 代价最优

#### 非代价最优算法的性能

####  


