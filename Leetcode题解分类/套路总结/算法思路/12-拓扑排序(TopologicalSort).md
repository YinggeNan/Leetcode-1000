1-Topological Sort (medium)
2-Tasks Scheduling (medium)
3-Tasks Scheduling Order (medium)
4-All Tasks Scheduling Orders (hard)
5-Alien Dictionary (hard)

## Course Schedule-medium
```
题目描述: 一个课程可能会先修课程，判断给定的课程学习顺序是否合法
思路:这是一个拓扑排序问题，只需要判定图里有无环就好，只有有向无环图DAG才有拓扑排序
获得拓扑排序的BFS算法是"图有n个节点，定义graph[n][n]和indgree[n]，graph[n][n]为图的邻接矩阵，indgreee[i]表示节点i的入度，
扫描图的所有边初始化raph[n][n]和indgree[n]，然后将indegree[i]为0的所有节点i加入到队列queue中，
从queue中poll出一个节点i，删除从i出发的所有边(将graph[i][n]>1的都减1），入度减少1之后为0的节点加入到queue中继续循环直到queue为空
queue中poll出的所有节点形成一个拓扑序列
本题只需要判断是否有环，所以不需要得到拓扑序列，只需要判定加入到queue中的节点数量是否等于n即可，等于n则无环
```
## Course Schedule II
```
描述: 得到拓扑排序
思路：和Course Schedule一样用BFS即可，不过DFS如何做呢？
```