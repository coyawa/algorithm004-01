# 学习总结

## 字典树（Trie）

核心思想是利用字符串的公共前缀来降低时间开销，达到空间换时间的效率提升。

字典树的特征：

- 节点不会存完整单词，而是字符
- 从根节点到某一节点，路径上经过的字符连接起来为该节点对应的字符串
- 每个节点的所有子节点路径代表的字符都不相同

## 并查集（DisjointSet/UnionFind）

一种树型的数据结构，用于处理一些不相交集合（Disjoint Sets）的合并及查询问题，比如组团和配对问题。

实现并查集需要实现的三种操作：

- makeSet(s)
- unionSet(x,y)
- find(x)

## 高级搜索的三种优化

### 剪枝

在朴素搜索的基础上，减少重复计算，或根据条件剪枝，尽早排除不可能的分支

### 双向BFS（Two-ended）

起点终点分别BFS，直到相遇

### 启发式搜索（A*算法）

根据问题特定的条件，使用优先队列代替BFS队列，优先扩散优先级高的，来引导搜索方向从而加速搜索过程
启发式估价函数: h(n)，根据问题特点，评价节点是否是所希望的解的可能性
如果简单以先入先出顺序为估价函数，则退化为简单BFS

## 二叉搜索树（Binary Search Tree）

定义：左子树的所有节点都小于根节点，右子树所有节点都小于根节点
查找效率和高度有关，即O(logn)
树和链表没有本质区别。二叉搜索树的极端情况：始终插入在一边，则会退化成链表，查找复杂度为O(n)
因此，为保证性能，需要维持BST的平衡性和二维维度，故引入平衡二叉树（有很多形式，比如AVL、红黑树、2-3树和B+树）

### AVL树

定义：平衡因子（balance factor）= 每个节点的左右子树高度差，最好保持在{-1, 0, 1}之间
通过旋转来进行平衡：

- 左旋
- 右旋
- 左右旋
- 右左旋

### 红黑树（Red-Black Tree）

一种近似平衡二叉树，确保任何一个节点左右子树的高度差小于两倍，具有以下特点：

- 每个节点要么是红色，要么是黑色
- 根节点是黑色
- 叶节点/空节点是黑色
- 红色节点不能相邻
- 从任一节点到其每个叶子节点的所有路径都包含相同数目的黑色节点

### 比较

AVL因为更严格平衡，故查找性能更好
RBT的添加和删除更快，因为需要维护的旋转操作更少
AVL需要存储factor，RBT只需要一个bit来存Red或Black的状态，因此存储空间更少
读操作多写操作少时用AVL（比如Database），否则用RBT（比如Map/Set的实现）