## Is Graph Bipartite?-medium
```
题目描述：判断是否是二分图
思路：一个二分图，任取一条边，总能把图的所有node分为两个set，则该边的node1在set1中，node2在set2中,
使用着色法，用两种颜色去给图的所有节点着色，对一个节点着色时，如果这个节点没有颜色那么用比如对node1着色blue(1)，
则对node1所有邻接点着色red(-1)，
```