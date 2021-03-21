### <a id="_link_click_group">LeetCode-广度优先遍历(BFS)-medium-题单</a>
##### [LeetCode-102.二叉树的层序遍历](#_id102)
##### [LeetCode-103.二叉树的锯齿形层序遍历](#_id103)
##### [LeetCode-107.二叉树的层序遍历II](#_id107)
##### [LeetCode-116.填充每个节点的下一个右侧节点指针](#_id116)
##### [LeetCode-130.被围绕的区域](#_id130)
##### [LeetCode-133.克隆图](#_id133)
##### [LeetCode-199.二叉树的右视图](#_id199)
##### [LeetCode-200.岛屿数量](#_id200)
##### [LeetCode-207.课程表](#_id207)
##### [LeetCode-210.课程表II](#_id210)
##### [LeetCode-261.以图判树](#_id261)
##### [LeetCode-279.完全平方数](#_id279)
##### [LeetCode-286.墙与门](#_id286)
##### [LeetCode-310.最小高度树](#_id310)
##### [LeetCode-314.二叉树的垂直遍历](#_id314)
##### [LeetCode-323.无向图中连通分量的数目](#_id323)
##### [LeetCode-417.太平洋大西洋水流问题](#_id417)
##### [LeetCode-429.N叉树的层序遍历](#_id429)
##### [LeetCode-490.迷宫](#_id490)

### 背景知识
1.树的BFS是很简单的,可以简单地理解为层次遍历    
2.图的BFS  
如果输入是所有的边,一般要建立每个节点的入度或出度数组,邻接表数组/邻接矩阵(表示一个图)  
图的BFS,从外层到内层: https://leetcode-cn.com/problems/minimum-height-trees/solution/zui-rong-yi-li-jie-de-bfsfen-xi-jian-dan-zhu-shi-x/  
### 从边缘向里BFS的题目:
LeetCode-130.被围绕的区域  
LeetCode-310.最小高度树  
LeetCode-417.太平洋大西洋水流问题  
### LeetCode-广度优先遍历(BFS)-medium-题解
##### <a id="_id102">[LeetCode-102.二叉树的层序遍历](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id103">[LeetCode-103.二叉树的锯齿形层序遍历](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id107">[LeetCode-107.二叉树的层序遍历II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id116">[LeetCode-116.填充每个节点的下一个右侧节点指针](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id130">[LeetCode-130.被围绕的区域](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id133">[LeetCode-133.克隆图](#_link_click_group)</a>
题目描述:
思路:先复制node的val，然后处理node邻接表，用一个map记录{oldNode:newOld}  
当map.get(node)为true时说明第二次访问到同一个节点了,这时就不能再次深度copy了
```
class Node {
    public int val;
    public List<Node> neighbors;
}
```
```
    // DFS 
    public Node cloneGraph(Node node) {
        if(node==null){
            return null;
        }
        Map<Node, Node> map = new HashMap<>();
        Node copyNode = new Node(node.val);
        map.put(node, copyNode);
        cloneGraph(node, copyNode, map);
        return copyNode;
    }
    // 把node的邻接表copy给copyNode
    public void cloneGraph(Node node, Node copyNode, Map<Node, Node> map){
        if(node.neighbors==null || node.neighbors.size()==0){
            return;
        }
        List<Node> copyNodeNeighbors = new ArrayList<>();
        copyNode.neighbors = copyNodeNeighbors;
        for(Node item: node.neighbors){
            if(map.containsKey(item)){
                copyNodeNeighbors.add(map.get(item));
            }else{
                Node tempNode = new Node(item.val);
                map.put(item, tempNode);
                copyNodeNeighbors.add(tempNode);
                cloneGraph(item, tempNode, map);
            }
        }
    }
```

```
    // BFS
    public Node cloneGraph(Node node) {
        if(node==null){
            return null;
        }
        Map<Node, Node> map = new HashMap<>();
        Node copyNode = new Node(node.val);
        // queu里放的是需要处理邻接表的节点
        Queue<Node> queue = new LinkedList<>();
        queue.add(node);
        map.put(node, copyNode);
        while(queue.size()>0){
            Node item = queue.poll();
            Node itemCopy = map.get(item);
            itemCopy.neighbors = new ArrayList<>();
            for(Node child: item.neighbors){
                // map中有了这个节点了,我们保证map中的key被放进map时就被放入了queue了
                // 所以不需要再次放入queue进行深度copy了
                if(map.containsKey(child)){
                    itemCopy.neighbors.add(map.get(child));
                }else{
                    Node childCopy = new Node(child.val);
                    map.put(child, childCopy);
                    itemCopy.neighbors.add(childCopy);
                    // child需要处理邻接点
                    queue.add(child);
                }
            }
        }
        return copyNode;
    }
```

##### <a id="_id199">[LeetCode-199.二叉树的右视图](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id200">[LeetCode-200.岛屿数量](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id207">[LeetCode-207.课程表](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id210">[LeetCode-210.课程表II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id261">[LeetCode-261.以图判树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id279">[LeetCode-279.完全平方数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id286">[LeetCode-286.墙与门](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id310">[LeetCode-310.最小高度树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id314">[LeetCode-314.二叉树的垂直遍历](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id323">[LeetCode-323.无向图中连通分量的数目](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id417">[LeetCode-417.太平洋大西洋水流问题](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id429">[LeetCode-429.N叉树的层序遍历](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id490">[LeetCode-490.迷宫](#_link_click_group)</a>
题目描述:
思路:
```

```
