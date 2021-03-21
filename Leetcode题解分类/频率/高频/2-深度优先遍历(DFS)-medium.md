### <a id="_link_click_group">LeetCode-深度优先遍历(DFS)-medium-题单</a>
##### [LeetCode-.电话号码的字母组合](#_id)
##### [LeetCode-98.验证二叉搜索树](#_id98)
##### [LeetCode-105.从前序与中序遍历序列构造二叉树](#_id105)
##### [LeetCode-106.从中序与后序遍历序列构造二叉树](#_id106)
##### [LeetCode-109.有序链表转换二叉搜索树](#_id109)
##### [LeetCode-113.路径总和II](#_id113)
##### [LeetCode-114.二叉树展开为链表](#_id114)
##### [LeetCode-116.填充每个节点的下一个右侧节点指针](#_id116)
##### [LeetCode-117.填充每个节点的下一个右侧节点指针II](#_id117)
##### [LeetCode-129.求根到叶子节点数字之和](#_id129)
##### [LeetCode-130.被围绕的区域](#_id130)
##### [LeetCode-131.分割回文串](#_id131)
##### [LeetCode-133.克隆图](#_id133)
##### [LeetCode-199.二叉树的右视图](#_id199)
##### [LeetCode-200.岛屿数量](#_id200)
##### [LeetCode-207.课程表](#_id207)
##### [LeetCode-210.课程表II](#_id210)
##### [LeetCode-211.添加与搜索单词](#_id211)
##### [LeetCode-261.以图判树](#_id261)
##### [LeetCode-314.二叉树的垂直遍历](#_id314)
##### [LeetCode-323.无向图中连通分量的数目](#_id323)
##### [LeetCode-332.重新安排行程](#_id332)
##### [LeetCode-337.打家劫舍III](#_id337)
##### [LeetCode-364.加权嵌套序列和II](#_id364)
##### [LeetCode-366.寻找二叉树的叶子节点](#_id366)
##### [LeetCode-394.字符串解码](#_id394)
##### [LeetCode-417.太平洋大西洋水流问题](#_id417)
##### [LeetCode-430.扁平化多级双向链表](#_id430)
##### [LeetCode-439.三元表达式解析器](#_id439)
##### [LeetCode-473.火柴拼正方形](#_id473)
##### [LeetCode-490.迷宫](#_id490)
##### [LeetCode-491.递增子序列](#_id491)
##### [LeetCode-494.目标和](#_id494)

### LeetCode-深度优先遍历(DFS)-medium-题解
##### <a id="_id">[LeetCode-.电话号码的字母组合](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id98">[LeetCode-98.验证二叉搜索树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id105">[LeetCode-105.从前序与中序遍历序列构造二叉树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id106">[LeetCode-106.从中序与后序遍历序列构造二叉树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id109">[LeetCode-109.有序链表转换二叉搜索树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id113">[LeetCode-113.路径总和II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id114">[LeetCode-114.二叉树展开为链表](#_link_click_group)</a>
题目描述:
思路:
```
      
    (1) 递归建立将先序遍历建立为链表
     // 全局链表尾指针
    TreeNode p = null;
    public void flatten(TreeNode root) {
        dfs(root);
    }
    // 空间复杂度O(N),递归栈最多N层
    public void dfs(TreeNode root){
        if(root==null){
            return;
        }
        // 保存root的right节点,因为在root的下一层root的right引用会被重置
        TreeNode right = root.right;
        // 保存root的left节点,因为root需要和root.left断开
        TreeNode left = root.left;
        // 断开 root和root.left
        root.left = null;
        if(p!=null){
            p.right = root;
        }
        p = root;
        dfs(left);
        dfs(right);
    }
    
    (2) 迭代
    // 迭代:如果node的left不为空,那么node的左子树的最右边的节点就是node的右子树的前驱
    // 所以先保存node的右子树为right,然后令node.left = node.right;
    // 然后遍历得到node左子树的最右边的节点rightestNode,然后令rightestNode.right = right
    // 对node的处理就结束了,然后处理下一个节点node.right
    // 一直到node的下一个节点为null为止
    // 参考:https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/solution/er-cha-shu-zhan-kai-wei-lian-biao-by-leetcode-solu/
    // 参考:https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--26/
    public void flatten(TreeNode root) {
        TreeNode p = root;
        while(p!=null){
            if(p.left==null){
                p = p.right;
                continue;
            }
            TreeNode rightestNode = p.left;
            while(rightestNode.right!=null){
                rightestNode =rightestNode.right;
            }
            rightestNode.right = p.right;
            p.right = p.left;
            p.left = null;
        }
    }
```
##### <a id="_id116">[LeetCode-116.填充每个节点的下一个右侧节点指针](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id117">[LeetCode-117.填充每个节点的下一个右侧节点指针II](#_link_click_group)</a>
题目描述:
思路: O(1)空间实现类似借助queue的BFS的效果,假设第i层已经建立了链表关系
从第i层的头节点开始遍历起可以遍历完第i层所有节点,  
由节点的left,right就可以遍历第i层节点建立第i+1层的链表关系  
关键是要有已经建立了链表关系的第i层的头节点,然后维护一个待建立链表关系的第i+1层的尾节点.  
```
    // 待建立的层已建立的链表的尾巴节点
    Node last = null;
    // 待遍历的层的第一个节点,比如要建立第i+1层节点,那么待遍历层就是第i层
    Node nextStart = null;
    // 每一层都要从左到右依次链接成为链表
    // 假设第i层已经从最左边到最右边的节点都链接成了链表
    // 那么对i+1层就可以遍历第i层节点来建立i+1层的链接关系
    public Node connect(Node root) {
        if(root==null){
            return null;
        }
        nextStart = root;
        // 外层循环循环一次移动到下一层遍历,类似于BFS
        while(nextStart!=null){ 
            Node p = nextStart;
            // 不让上一层的last引用影响本层last
            last = null;
            // 不让上一层的nextStart影响本层nextStart
            nextStart = null;
            // 遍历链表代替在queue中遍历,一样控制了遍历顺序
            for(;p!=null;p=p.next){
                if(p.left!=null){
                    setNext(p.left);
                }
                if(p.right!=null){
                    setNext(p.right);
                }
            }
        }
        return root;
    }

    public void setNext(Node node){
        // 待建立层的第一个节点,是建立下一层时要访问的链表头节点
        if(last==null){
            nextStart = node;
        }
        // 排除待建立层的第一个节点
        if(last!=null){
            last.next = node;
        }
        last = node;
    }
```
##### <a id="_id129">[LeetCode-129.求根到叶子节点数字之和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id130">[LeetCode-130.被围绕的区域](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id131">[LeetCode-131.分割回文串](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id133">[LeetCode-133.克隆图](#_link_click_group)</a>
题目描述:
思路:
```

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
##### <a id="_id211">[LeetCode-211.添加与搜索单词](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id261">[LeetCode-261.以图判树](#_link_click_group)</a>
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
##### <a id="_id332">[LeetCode-332.重新安排行程](#_link_click_group)</a>
题目描述:  题目说明了给的输入一定存在欧拉回路，则需要寻找一个欧拉回路/通路  
通路/回路的定义:https://blog.csdn.net/qq_21774161/article/details/103063860  
思路:
```
    // hieholzer算法
    // 深度优先遍历,每次都先搜索完后node的所有出度节点后才将node入栈
    // 只有当一个节点没有路径可走时才将其入栈
    // 从node出发，对所有非死胡同节点都能回到node,而非死胡同节点不能回到node
    // 所以非死胡同节点一定第一个入栈,
    // 一笔画问题,所有的边只走一次，而且经过所有的节点
    // 有向欧拉图最多只有一个顶点的入度和出度差1
    public List<String> findItinerary(List<List<String>> tickets) {
        // 和node相连的每个节点放入优先队列里按照字典序排列.
        Map<String, PriorityQueue<String>> map = new HashMap<>();
        List<String> res = new ArrayList<>();
        for(List<String> item: tickets){
            if(!map.containsKey(item.get(0))){
                map.put(item.get(0), new PriorityQueue<String>());
            }
            map.get(item.get(0)).add(item.get(1));
        }
        dfs(map, "JFK", res);
        Collections.reverse(res);
        return res;
    }
    public void dfs(Map<String, PriorityQueue<String>> map, String node, List<String> res){
        while(map.containsKey(node) && map.get(node).size()>0){
            String out = map.get(node).poll();
            dfs(map, out, res);
        }
        res.add(node);
    }
```
##### <a id="_id337">[LeetCode-337.打家劫舍III](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id364">[LeetCode-364.加权嵌套序列和II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id366">[LeetCode-366.寻找二叉树的叶子节点](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id394">[LeetCode-394.字符串解码](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id417">[LeetCode-417.太平洋大西洋水流问题](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id430">[LeetCode-430.扁平化多级双向链表](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id439">[LeetCode-439.三元表达式解析器](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id473">[LeetCode-473.火柴拼正方形](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id490">[LeetCode-490.迷宫](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id491">[LeetCode-491.递增子序列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id494">[LeetCode-494.目标和](#_link_click_group)</a>
题目描述:
思路:
```

```
