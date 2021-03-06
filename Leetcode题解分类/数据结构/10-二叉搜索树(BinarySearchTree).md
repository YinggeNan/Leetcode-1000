## Convert Sorted Array to Binary Search Tree (Easy)

题目描述: 从有序数组中构造平衡的BST  

思路: 对有序数组二分，mid为root的值，[low, mid-1]范围的为左子树的值，[mid+1, high]范围的为右子树的值，对左右子树也构建平衡BST  

## Convert Sorted List to Binary Search Tree (Medium)

题目描述: 从有序链表构造平衡的二BST  

思路: 对以head开头的有序链表二分(用快慢指针)，要得到链表中点mid的父指针pre，mid为root的值，[head,pre]范围为左子树的值，[mid,tail]范围为右子树的值，对左右子树也构建平衡BST  

*** 注意要得到链表中点mid的父指针pre，因为要将pre和mid之间截断，这样才能在对[head,pre]范围的链表正确得到mid节点  

## Two Sum IV - Input is a BST (Easy)

题目描述: 在二叉查找树中寻找两个节点，使它们的和为一个给定值  

思路: 中序遍历BST得到递增序列nums，对nums使用双指针夹逼法求和为给定值的pair

## Minimum Absolute Difference in BST (Easy)

题目描述: 在二叉查找树中查找两个节点之差的最小绝对值  

思路: 中序遍历BST得到递增序列nums，遍历nums对每对相邻的pair计算绝对值得到最小绝对值  


## Find Mode in Binary Search Tree (Easy)

题目描述: 寻找二叉查找树中出现次数最多的值  

思路: 中序遍历BST得到递增序列nums，遍历nums统计每个数出现的频率，设置maxCount(全局最高频率)和curCount(当前连续数字最高频率)，得到最大频率
