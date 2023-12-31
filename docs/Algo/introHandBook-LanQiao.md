# 算法竞赛入门大纲（蓝桥向）

## 学习资料

### [OI-wiki](https://oi-wiki.org/)

可以当教材也可以当工具书，OI-er 最好用的日常材料。

## 算法数据结构大纲

### 算法

1. 时间复杂度和空间复杂度：不是算法，属于必须掌握的算法基础，在估计做法的时候极其常用。
2. 暴力和模拟、枚举等：不是算法或者简单算法，基本只考逻辑转化为代码的能力，蓝桥杯极其通用常见（且蓝桥存在感逐步下降）。
3. 滑动窗口和双指针：基础入门算法
4. 递归、回溯：重要算法思想
5. 排序：不考实现，需要掌握用法，很多题会用到，要知道排序算法的时间复杂度。
6. 二分（二分查找和二分答案）：基础算法有几种不同套路，难度一般，蓝桥存在感不强。
7. 搜索算法（广度优先搜索 BFS 和深度优先搜索 DFS，迪杰斯特拉（最短路算法））：蓝桥杯很常见，BFS 和 DFS 必会，Dijkstra 可以不会。
8. 贪心：没有模板，本质是算法思想，基础算法题中贪心出现频率非常高。
9. 前缀和、差分：常用的代码技巧
10. 数学（多是数论）：范围很广，除了力扣之外存在感很强，蓝桥杯有一些要求但不多（近年存在感渐强），强烈建议学习！
11. 位运算：存在感不强，要求不高，但要掌握基础。
12. 动态规划：进阶算法，但是在各种算法竞赛中存在感极强（不代表出现频率），蓝桥杯要求不太高（存在感渐强）。

上述算法全部都要理解并掌握基础，越靠后的部分的要求会稍微低一点点，但都要求基本掌握。

备战蓝桥，在掌握所有的基础上，进阶贪心、暴力、模拟、搜索等算法，要专门练习数学数论题（懂的要多，可以不精通）。

### 数据结构

1. 数组和矩阵
2. 集合
3. 哈希表
4. 二叉树
5. 字符串：不算数据结构，接近数组，不同语言写法不同，存在感很强
6. 链表
7. 栈
8. 树
9. 堆和优先队列
10. 并查集
11. 图

上述结构中，语言内置的基础数据结构用法必须熟悉。同时，树、字符串、链表、栈、图都要学习熟练。

## 常用容器

算法题会用到大量的数据结构，有些数据结构是离散数学里定义的（如二叉树、并查集），还有些基础数据结构是在语言里内置的，每个语言都会有，这种数据结构最常用，最经典的就是数组（列表），哈希表（又叫字典），集合（哈希集），堆和栈和队列（很多时候会用数组加额外函数实现），很多语言中也会使用元组（tuple）。

### 数组

最基础的数据结构，竞赛常用的数组通常不是语言默认的那个数组，而是标准库里一般都有的可变长数组，通常用 vector、list、arraylist 表示这种数组。一般都是引用类型而非值类型，特点是可以延长以存储更多值，可以添加和删除元素。

### 集合、哈希表

哈希表是存储键值对的数据结构，就像字典一样一个单词对应一个释义，哈希表中一个键（key）对应着一个值（value）。

哈希表的优势是查询起来很快速（复杂度：常数级），而且键值对存储本身就很有用。

集合是类似没有值的哈希表，本身类似一个数组，存储同类型的多个不同数据，数据之间不重复。

集合的作用是去重。

### 堆、栈、队列

比赛中基本不会考验堆和栈的实现，只考使用，考堆的使用的时候考的一般都是优先队列。

栈的结构类似一个变长数组（vector），只有两种操作，一个是在末尾添加元素，一个是在末尾取出元素，可以想象成一个网球筒。

队列类似一个栈，普通的队列可以在末尾添加元素，在开头取出元素，就像排队一样。很多语言实现都支持了双端队列，就是两头都可以添加或者取出的队列。

堆一般都会用作优先队列，优先队列是一个队列，新加入元素的时候，会按照大小顺序把元素插入到合适的地方。

优先队列的功能是维持一个树（用数组实现），可以永远用常数级时间复杂度来取出整个堆中最大或最小的数。

堆有两种，一个是从小到大，一个是从大到小，每次能取出最大的数的叫大根堆，每次取最小的叫小根堆。

优先队列很适合贪心，因为可以做到在加数据的同时排序。

## 离散数学中的数据结构

就是一般意义上说的算法中的数据结构，这些结构撑起了离散数学的半壁江山。

### 链表

数据结构梦开始的地方。链表是最基础的顺序表（就是像数组一样顺序固定的表）。

链表用节点结构实现，每个节点包括了一个值和指向下一个节点的指针。链表的末尾节点不会指向另一个节点，所以用空指针或者空对象表示。

你可以把链表想象成曹老板的铁索连舟，一艘船连着一艘船，每艘船上都装着一箱粮草辎重，还有一条锁链连着下一艘船。

一般使用的时候只会给你第一艘船，你要去第二艘船，你就要从第一艘船走上来，顺着铁索走上第二条船。而不能直接跨到之后的船上。

链表一般不会考应用，要考就是链表操作熟练度。要会链表的插入（在两艘船中间加一艘船），删除，修改，连接等等。著名题目有反转链表、合并链表等等。

此外还有双向链表、循环链表、跳跃表等，但存在感不强。

### 二叉树

连接方式类似链表，只不过这次的链表每艘船连着两条链子，连到两艘船上。
