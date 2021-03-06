#lec9: 虚存置换算法spoc练习

## 视频相关思考题

### 9.1 页面置换算法的概念

1. 设计置换算法时需要考虑哪些影响因素？如何评判的好坏？

   目标：尽可能减少页面的调入调出次数

   影响因素：进程的页面访问规律（访问模式、访问频度）

   评判标准：记录并统计产生缺页的次数

2. 全局和局部置换算法的不同？

   局部置换是在当前进程占用的物理页面范围内置换；

   全局置换是基于不同进程的物理页面需求是不同的，在所有可换出的物理页面范围内置换；

### 9.2 最优算法、先进先出算法和最近最久未使用算法

1. 最优算法、先进先出算法和LRU算法的思路？

   最优：置换在未来最长时间不访问的页面

   先进先出：选择在内存中驻留时间最长的页面进行置换

   LRU：选择最长时间没有被引用的页面进行置换

### 9.3 时钟置换算法和最不常用算法

1. 时钟置换算法的思路？

   仅对页面的访问情况进行大致统计

2. 改进的时钟置换算法与时钟置换算法有什么不同？

   增加修改位，以减少缺页处理开销（缺页时直接跳过修改过的页面）

3. LFU算法的思路？

   页面队列的排序指标是过去的页面访问次数


### 9.4 Belady现象和局部置换算法比较

1. 什么是Belady现象？如何判断一种置换算法是否存在Belady现象？

   分配的物理页面增加，缺页次数也增加

   构造反例或证明是栈式置换算法

2. 请证明LRU算法不存在Belady现象。

   最优置换和LRU算法都没有Belady异常。这两个都属于同一类算法，称为栈算法（stack algorithm），都绝不可能有Belady异常。栈算法可以证明为：对于帧数为n的内存页集合是对于帧数为n+1的内存页集合的子集。对于LRU算法，如果内存页的集合为最近引用的页，那么对于帧的增加，这n页仍然是最近引用的页，所以也仍然在内存中。

### 9.5 工作集置换算法

1. CPU利用率与并发进程数的关系是什么？

   进程数少时，CPU利用率与并发进程数会相互促进；

   进程数较多导致局部性降低时，CPU利用率与并发进程数会相互制约；

2. 什么是工作集？

   当前进程正在使用的逻辑页面的集合

3. 什么是常驻集？

   当前时刻进程实际驻留内存的页面集合

4. 工作集算法的思路？

   把不在工作集的页面置换到外存；

### 9.6 缺页率置换算法

1. 缺页率算法的思路？

   保持适度的缺页率。即缺页率过高时增加常驻集，缺页率过低时减少常驻集

### 9.7 抖动和负载控制

1. 什么是虚拟内存管理的抖动现象？

   抖动现象是指，由于分配给进程的物理页面太少导致频繁置换，从而进程运行速度变慢；

2. 操作系统负载控制的最佳状态是什么状态？

   平均缺页间隔 = 缺页异常处理时间。

3. 局部置换算法（如FIFO, LRU等）是否能作为全局置换算法来使用？为什么？

   局部置换算法不能作为全局置换算法使用,进程切换会导致进程占用的页面被全部换出.

----

## 扩展思考题

1.  改进时钟置换算法的极端情况: 如果所有的页面都被修改过了，这时需要分配新的页面时，算法的performance会如何？能否改进在保证正确的前提下提高缺页中断的处理时间？

2.  如何设计改进时钟算法的写回策略?

3. （spoc）根据你的`学号 mod 4`的结果值，确定选择四种页面置换算法（0：LRU置换算法，1:改进的clock 页置换算法，2：工作集页置换算法，3：缺页率置换算法）中的一种来设计一个应用程序（可基于python, ruby, C, C++，LISP等）模拟实现，并给出测试用例和测试结果。请参考如python代码或独自实现。
 - [页置换算法实现的参考实例](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab3/page-replacement-policy.py)     

4. 请判断OPT、LRU、FIFO、Clock和LFU等各页面置换算法是否存在Belady现象？如果存在，给出实例；如果不存在，给出证明。

5. 了解LIRS页置换算法的设计思路，尝试用高级语言实现其基本思路。此算法是江松博士（导师：张晓东博士）设计完成的，非常不错！
	- 参考信息：
 	- [LIRS conf paper](http://www.ece.eng.wayne.edu/~sjiang/pubs/papers/jiang02_LIRS.pdf)
	 - [LIRS journal paper](http://www.ece.eng.wayne.edu/~sjiang/pubs/papers/jiang05_LIRS.pdf)
	 - [LIRS-replacement ppt1](http://dragonstar.ict.ac.cn/course_09/XD_Zhang/(6)-LIRS-replacement.pdf)
	 - [LIRS-replacement ppt2](http://www.ece.eng.wayne.edu/~sjiang/Projects/LIRS/sig02.ppt)
