#### 2021-1-05
## Maximum Depth of Binary Tree (Easy)
题目描述:  给一颗二叉树，求其高度

思路: 树高度 = Math.max(左子树高度,右子树高度) + 1，定义递归函数maxDepth(TreeNode node)返回root节点深度
## Balanced Binary Tree (Easy)
题目描述: 给一颗二叉树，判断其是否为平衡树

尝试：定义isHeight(root)返回以root为根节点的二叉树是否平衡，这时假定得到了isHeight(root.left)和isHeight(root.right)，但是就算root左子树和root右子树都平衡，也无法判定root是否平衡  
比如root左子树平衡但是最大深度为2，root右子树平衡但最大深度为5，这时我们root不平衡；所以此定义是不合理的  

思路: 判断平衡树的每一个节点的左右子树的差值都不超过1即可，关键是得到每个节点的左右子树高度  
&nbsp;解法1：遍历每个节点，遍历到该节点时求其左右子树高度差，时间复杂度很高大概为O(N*logN)  
&nbsp;解法2：修改求树高度的递归函数maxDepth，让其在得到得到左右子树高度的同时判断高度差是否满足小于等于1即可  

## Diameter of Binary Tree (Easy)
题目描述: 给一颗二叉树，求其中任意两个节点之间的的最长路径长度，这个路径不一定要经过该树的根节点

尝试：定义maxPathLength(root)返回以root为根节点的任意两个节点之间的的最长路径长度，假定得到maxPathLength(root.left)和maxPathLength(root.right), 也无法计算得到maxPathLength(root)，  
因为最长的路径是从root.left的左子树最低层节点经过root.left然后到root.right最底层的节点，所以此定义不合理

思路: 只能得到经过每个节点的最长路径，然后取最大值，因为最长路径一定经过了某个子树的根节点，所以求得所有子树中经过了本子树根节点的最长路径，并取其中最长的最长路径者的长度即为答案
&nbsp;&nbsp;经过node的最长路径 = node左子树高度 + node右子树高度(一个节点高度为1)， 设置一个全局变量maxPathLength，
&nbsp;&nbsp;修改求树高度的递归函数maxDepth，让其在得到节点node的左右子树高度的时计算经过node的最长路径nodeMaxPathLength并更新全局maxPathLength
## Invert Binary Tree (Easy)
题目描述: 给一颗二叉树，翻转其所有节点

思路: 将每一个节点的左右子树交换
&nbsp;&nbsp;定义递归函数invertTree(TreeNode root)返回将以root为根节点的树交换后的根节点，注意invertTree(root.left)表示将以root.left为根节点的左子树交换，  
&nbsp;&nbsp;但root的左右子节点root.left和root.right的交换应该在上一层以root为参数的函数中实现，
```
    // 解法1: 交换操作从下层->上层
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode left = root.left;  // 后面的操作会改变 left 指针，因此先保存下来
        root.left = invertTree(root.right); //左右子树交换
        root.right = invertTree(left); //左右子树交换
        return root;
    }
```
```
    // 解法2: 交换操作从上层->下层
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;
        }
        TreeNode temp = root.left; 
        root.left = root.right;
        root.right = temp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
```
## Merge Two Binary Trees (Easy)
题目描述: 给两颗二叉树s、t，归并s、t为一颗新树，要求当同一位置s没有节点而t有节点i时i直接为新树的该位置节点，同一位置s无而t有节点一样，而同一位置s、t分别有节点x、y时，新树该位置节点值为x.val+y.val

思路:  
&nbsp;&nbsp;定义递归函数merge(TreeNode s, TreeNode t)返回分别以s、t为根节点的两棵树的merge的新树  
&nbsp;&nbsp;以两个指针遍历t1、t2，每次t1、t2都分别指向s、t的同一位置的节点  
&nbsp;&nbsp;对k位置来说：定义newTree-k、s-k、t-k分别表示新树、s、t在k位置的节点  
&nbsp;&nbsp;当s-k为null，t-k不为null时，newTree-k = t-k;  
&nbsp;&nbsp;当s-k不为null，t-k为null时，newTree-k = s-k;  
&nbsp;&nbsp;当s-k不为null且t-k不为null时:  
&nbsp;&nbsp;s-k.val += t-k.val; // 将s-k节点重复使用，作为新树k位置节点  
&nbsp;&nbsp;newTree-k = s-k;  
&nbsp;&nbsp;newTree-k.left = merge(s-k.left, t-k.left); // 对s-k、t-k的左子树merge后作为newNode的左子树  
&nbsp;&nbsp;newTree-k.right = merge(s-k.right, t-k.right); // 对s-k、t-k的右子树merge后作为newNode的右子树  

## Path Sum (Easy)
题目描述: 给一个二叉树和一个数sum，判断该二叉树中是否存在一条从根节点到叶子节点的路径，使得该路径上的所有节点值的累加和等于该数sum

尝试：定义pathSum(root, sum)返回在以root为根节点的二叉树中是否存在一条路径使得路径上所有节点累计和等于sum，假定得到leftFlag = pathSum(root.left, sum - root.val)和 rightFlag = pathSum(root.right, sum -root.val)
只要leftFlag || rightFlag 为true就说明root左子树或右子树存在一条路径使得路径上节点值累计和为sum-root.val，再加上root.val不就是sum了吗

递归函数定义时，考虑路径累计和如何计算：
&nbsp;&nbsp;(1) 不能从叶子节点向上传从叶子节点到root节点路径累计和，因为需要返回一个list来保存每个不同路径的累计和
&nbsp;&nbsp;(2) 应该从根节点向下传已经遍历过的路径累计和
``` 
    // 递归过程枚举了所有从根节点到叶子节点的路径并计算路径和，只要有一条路径的累加和等于给定的数则满足条件
    public boolean pathSum(TreeNode root, int target){
        // root == null时，root为叶子叶子的左右空指针，继然叶子节点没有返回true这里就应该返回false
        // 或者root为非叶子节点的某个空指针孩子，也应该返回false
        if(root == null){
            return false;
        }
        // 叶子节点, 且root-to-leaf路径和等于target
        if(root.left==null && root.right==null && target==root.val){
            return true;
        }
        return pathSum(root.left, target-root.val) || pathSum(root.right, target-root.val);
    }
```
```
    // 解法2
    private boolean flag = false;
    public void pathSum(TreeNode root, int currentSum, int sum){
        // 说明root前面的节点都没有返回true，则这里肯定不满足条件了
        if(root == null){
            return;
        }
        currentSum += root.val;
        if(root.left==null && root.right==null && currentSum==sum){
            flag = true;
        }
        pathSum(root.left, currentSum, sum);
        pathSum(root.right, currentSum, sum);
    }
```
## Path Sum III
题目描述: 给一个二叉树和一个数num，找到并返回所有满足规定条件的路径的数量, 要求路径可以不从root节点开始，也可以不以叶子节点结束，但必须一直向下延展，且路径上所有节点值累计和等于给定的树num  
例子: 对节点node，若node.left、node.right存在，则路径node.left->node->node.right不符合一直向下延展的规定

尝试：定义pathSum(root, sum)返回在以root为根节点的二叉树中所有满足条件的路径的数量，假定得到了左子树所有满足条件的路径数量allLeft = pathSum(root.left, sum)和右子树所有满足条件的路径数量allRight = pathSum(root.right, sum)  
我们也无法计算pathSum(root, sum)的值，因为很可能在左子树中有一条从root.left向下延申一条路径和等于sum-root.val，但是我们并不知道是否存在多少条

思路:  定义pathSumStartWithRoot(TreeNode root, int sum)返回从root节点开始向下的所有路径节点值和累计为sum的路径数量，对树中所有节点施加pathSumStartWithRoot(node, sum)统计即可
(1)全局变量:https://leetcode.com/submissions/detail/438932880/  
(2) 
``` 
    // 遍历以root树中的所有节点，返回所有节点pathSumStartWithRoot(node, sum)的和
    public int pathSum(TreeNode root, int sum) {
        if (root == null) return 0;
        int ret = pathSumStartWithRoot(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
        return ret;
    }
    private int pathSumStartWithRoot(TreeNode root, int sum) {
        if (root == null) return 0;
        int ret = 0;
        if (root.val == sum) ret++;
        ret += pathSumStartWithRoot(root.left, sum - root.val) + pathSumStartWithRoot(root.right, sum - root.val);
        return ret;
    }
```
# 2021-1-06
## Subtree of Another Tree
题目描述: 给两颗二叉树s、t，判断是否存在s的一颗子树s1，让s1和t的结构，对应位置的节点值完全一样，s的子树的定义为s的任意的一个节点和该节点的所有后代子节点形成的树  
思路:
## Symmetric Tree 
题目描述: 给一颗二叉树，判断其是否为左右对称，既从中线折叠后可以重合(折叠后相同位置节点值相同)  
思路: 
## Minimum Depth of Binary Tree 
题目描述: 给一棵二叉树，求其最小深度，深度定义为从根节点到任意一个叶子节点的路径长度(路径节点数-1)  
思路:
## Sum of Left Leaves
题目描述: 给一棵二叉树，求其所有"左叶子"节点值的累加和  
思路: 满足条件的节点必须是左节点，且是叶子节点
## Longest Univalue Path
题目描述: 给一颗二叉树，求二叉树中的最长路径的长度(路径上节点数量-1)，这个路径不需要经过该树的根节点，也不一定要经过任意一个父节点，但这个路径中的每个节点值都必须一样  

思路:
## House Robber III
题目描述: 给一棵二叉树，每个节点代表一个房子，小偷从根节点开始偷窃，规则是不能偷窃直接相连的两个节点，否则小偷会被抓住，除了根节点无父节点外其他节点有且只有一个父节点  

思路:
## Second Minimum Node In a Binary Tree
题目描述: 找出二叉树中第二小的节点，所给二叉树满足，每个节点要嘛有0个孩子，要嘛有两个孩子，且有两个孩子的父节点parent的值parent.val = Math.min(leftChild.val, rightChild.val)  

思路:
# 2021-1-06
## Average of Levels in Binary Tree (Easy)
题目描述: 求二叉树的每层平均节点数量  
思路: queue+while层次遍历，在遍历当前层时queue.size()就是当前层的节点数量  
## Find Bottom Left Tree Value (Easy)
题目描述: 找到二叉树中最底的那一层的最左边的节点   
思路: 层次遍历，最后一层第一个节点
## Binary Tree Inorder Traversal (Medium)
题目描述: 非递归实现中序遍历  
思路: stakc + while  
1-循环：
while (root!=null || !stack.isEmpty())
&nbsp;&nbsp;1.root不为空时沿着root左子树方向将所有节点加入stack
&nbsp;&nbsp;2.stack弹出一个节点node, visit(node)
&nbsp;&nbsp;3.root = node.right，返回到1
## Binary Tree Preorder Traversal
题目描述: 非递归实现前序遍历  
思路: stack + while 
1-循环：
while (root!=null || !stack.isEmpty())
&nbsp;&nbsp;(1) root不为空时沿着root左子树方向将所有节点加入stack，加入一个节点node就visit(node)
&nbsp;&nbsp;(2) stack弹出一个节点node, root = node.right，返回到1

## Binary Tree Postorder Traversal (Medium)
题目描述: 非递归实现前序遍历  
思路: 先得到根、右、左序列，然后逆序得到左、右、根序列; stakc + while
1-循环：
while (root!=null || !stack.isEmpty())
&nbsp;1.root不为空时沿着root右子树方向将所有节点加入stack，加入一个节点node就visit(node)
&nbsp;2.stack弹出一个节点node, root = node.left，返回到1
2-将得到的序列逆序,Collections.reverse()
# 2021-1-07
## Trim a Binary Search Tree (Easy)
题目描述: 对BST执行裁剪操作，给定一个范围[low,high]，将BST中节点值不在此范围的节点删除，返回裁剪后的根节点  
思路: BST的特性是 "对任意一个node，node左子树所有节点的值 < node.val < node右子树所有节点的值", 所以如果node.val<low，则node的左子树都需要被裁剪掉, node.val>high，则node右子树都需要被裁剪掉     
node.val在[low,high]范围内时，node应该保留，然后对左子树和右子树执行保留操作
## Kth Smallest Element in a BST (Medium)
题目描述: 寻找二叉查找树的第k小的节点的值  
思路:   
&nbsp;(1)中序遍历二叉树能得到递增排序的序列，所以得到的第k个节点就是第k小的节点  
&nbsp;2)定义一个递归函数f(TreeNode root, k)返回以root开头的BST的第k小元素，定义一个递归函数count(f(TreeNode root)统计以root开头的二叉树的节点总数量   
&nbsp;&nbsp;&nbsp;&nbsp;如果count(root.left)为k-1，那么根据BST的左子树节点值<根节点值<右子树节点值特性可得到root就是第k小的节点  
&nbsp;&nbsp;如果count(root.left)<k-1，那么第k小的节点必然在右子树中，设此时左子树节点数量+1个root节点为leftNumber = count(root.left)+1, 所以搜索范围缩小，问题转移为求f(root.right, k-leftNumber)  
&nbsp;&nbsp;如果count(root.left)>k-1,那么低k小的节点必然在左子树中，问题转移为求f(root.left, k)  

## Convert BST to Greater Tree (Easy)

题目描述: 把二叉查找树每个节点的值都加上所有比它大的节点的值  
思路: 对BST进行"右->根->左"顺序的遍历能得到递减的序列，所以对BST进行右->根->左遍历，并累加每个节点的值为sum，遍历到每个节点node时sum就是比node值大的所有节点值之和  

# 2021-1-08
## Lowest Common Ancestor of a Binary Search Tree (Easy)

题目描述: 在二叉查找树中求节点p、q的最近公共祖先  
前置考虑:  
&nbsp;&nbsp;1. p、q的最近公共祖先的情况(1)p、q在节点node的左右子树中(2)p为q祖先或q为p祖先  
&nbsp;&nbsp;2.p、q在以root为根节点的BST中的相对root的可能分布情况(1)p、q在root的左或右子树中(2)p、q分别在root的左右子树中(3)q或q为root  
思路:  
&nbsp;&nbsp;定义递归函数findLowestAncester(TreeNode root, reeNode p, reeNode q)返回在以root为根节点的BST中的p、q最近公共祖先  
&nbsp;&nbsp;1.通过p、q的val判定q、q都在root左子树或root右子树中(p、q的val都小于root.val或大于root.val时)，问题转化为findLowestAncester(root.left, p, q)或findLowestAncester(root.right, p, q)   
&nbsp;&nbsp;2.通过p、q的val判定p、q分别在root的左右子树中,root就是最近公共祖先  
&nbsp;&nbsp;3.p或q为root时，root就是最近公共祖先  

## Lowest Common Ancestor of a Binary Tree (Medium)

题目描述: 在二叉树中求节点p、q的最近公共祖先  
前置考虑:  
&nbsp;&nbsp;1. p、q的最近公共祖先的情况(1)p、q在节点node的左右子树中(2)p为q祖先或q为p祖先  
&nbsp;&nbsp;2.p、q在以root为根节点的二叉树中的相对root的可能分布情况(1)p、q在root的左或右子树中(2)p、q分别在root的左右子树中(3)q或q为root  
思路:   
&nbsp;&nbsp;定义递归函数findLowestAncester(TreeNode root, reeNode p, reeNode q)返回在以root为根节点的BST中的p、q最近公共祖先或p、q节点，返回null时表示找不到最近公共祖先节点  
&nbsp;&nbsp;1.p或q为root节点时，返回root(此时root为递归函数第一层调用时是最近公共祖先节点，为更底层调用时可能是最近公共祖先节点或p、q节点)  
&nbsp;&nbsp;2.搜索左右子树leftNode = findLowestAncester(root.left, p, q),搜索右子树rightNode = findLowestAncester(root.right, p, q)  
&nbsp;&nbsp;leftNode为null时，那么最近公共祖先节点在root右子树中  
&nbsp;&nbsp;rightNode为null时，那么最近公共祖先节点在root左子树中  
&nbsp;&nbsp;leftNode、right都不为null时，root为最近公共祖先节点为      
