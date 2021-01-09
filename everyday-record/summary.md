##### 1.在以root为根节点的二叉树中，返回所有以root开始并且路径和等于给定值sum的路径数量：
#####//解法1
```
    public int pathSumWithRoot(TreeNode root, int sum){
        if(root==null){
            return 0;
        }
        int ret = 0;
        if(root.val==sum){
            ret++;
        }
        int nextSum = sum-root.val;
        ret += pathSumWithRoot(root.left, nextSum) + pathSumWithRoot(root.left, nextSum);
    }
```
#####//解法2：使用全局变量ret，不过这种解法没有解法1精妙
```
    private int pathNumber = 0;
    public void hasPathFromRoot(TreeNode root, int sum){
        if(root==null){
            return;
        }
        if(root.val == sum){
            pathNumber++;
        }
        sum = sum-root.val;
        hasPathFromRoot(root.left, sum);
        hasPathFromRoot(root.right, sum);
    }
```
#### 2.在以root为根节点的二叉树中，判断是否存在以root开始并且路径和等于给定值sum的路径
```
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null){
            return false;
        }
        if(root.val==sum){
            return true;
        }
        int nextSum = sum - root.val;
        return hasPathSum(root.left, nextSum) || hasPathSum(root.right, nextSum);
    }
```
##### 3.树结构很适合写递归的解法，因为树本身就是递归定义的
###### (1)抽象思维
解决很多题目时，就是抽象的思考题目的意思，并不需要考虑是前序、中序、还是后序地去遍历树中的节点
比如"求树的高度这道题目"(Maximum Depth of Binary Tree)，正确的思考方式就是树高 = 1 + Math.max(左子树高+右子树高)，这就是一个前序遍历，
但是这是不是前序遍历并不重要，所以如果题目规定必须采用前序、中序、后续中的某一种来解决，就不需要考虑遍历顺序
###### (2)全局变量+递归函数
全局变量+递归函数：
有返回值的递归函数：递归函数的返回值只是为了完成递归函数的工作的中间产物，这和我们通常写的函数有些区别
不管是有返回值的递归还是void递归函数，全局变量才是递归函数的最终结果
###### (3)树结构题目-可能的三种写法
1.void递归函数+全局变量：全局变量才是最终结果
2.有返回值的递归函数：返回值是最终结果
3.有返回值的递归函数+全局变量：全局变量才是最终结果
比如题目 Path Sum III
##### (4)如何确定在递归函数f体中调用f的顺序
a.问题要求显式地以前、中、后序遍历这个树的所有节点时，以标准的前、中、后递归函数写法遍历即可
b.为了完成定义的递归函数的功能时必须按照某种顺序，这个顺序是由思路来决定的
例子：比如LC671-Second Minimum Node In a Binary Tree
    题目描述：给定一颗二叉树，满足一个节点要嘛只有2个子节点且父节点值为两个子节点中最小者，要嘛为叶子节点，求树中第二小的节点的值，也就是大于根节点的最小节点的值
    重点：当root的节点有左右孩子时，如果root.left.val>root.val也不能说明root.left就是答案，因为在root的右子树中还有可能存在值大于root.val但是小于root.left.val的节点
        所以此时leftMin必须等到findSecondMinimumValue(root.right)执行完毕可以比较大小返回
```
    // 定义findSecondMinimumValue为返回以root为根节点的树中大于root节点值的最小值节点的值
    // 对以node为根节点的子树而言，f(node)返回的是比node大于的最小节点,而对node本身是否就是所求节点，必须在f(node's parent)中判断
    // 返回-1表示找不到比根节点root大的最小的节点
    // 如果一个节点root不是叶子节点那么必然有两个子节点
    public int findSecondMinimumValue(TreeNode root) {
        // 叶子节点和空节点
        if(root == null || (root.left==null && root.right==null)){
            return -1;
        }
        int leftMin = 0;
        int rightMin = 0;
        // 取的左右子树中大于root的最小值
        if(root.left.val == root.val){
            //
            leftMin = findSecondMinimumValue(root.left);
        }else{
            leftMin = root.left.val;
        }
        if(root.right.val == root.val){
            rightMin = findSecondMinimumValue(root.right);
        }else{
            rightMin = root.right.val;
        }
        return leftMin==-1?rightMin:rightMin==-1?leftMin:Math.min(leftMin, rightMin);
    }
```

当解决一个
这时就可以来考虑是前序、后续、中序了，不过都一样
##### (5)对于路径类题目，计算路径长度或计算路径上所有节点val和时
1.给递归函数传入父节点累计和
2.对子节点调用递归函数时，将目标sum更新为sum-父节点累计和
##### (6)路径类问题，对于从root节点出发且可能会多个符合条件的返回值递归函数写法

##### (7)树类问题，第一关键是思路(难点的题目思路比较复杂)，第二关键是对于code，定义好递归函数的返回值和递归函数的作用
##### (8)树类问题，递归函数的定义就是数学模型的定义，对于有返回值的递归函数这个返回值是什么很关键，返回值可能就是最终结果，也可能只是为了递归函数真正的工作做准备