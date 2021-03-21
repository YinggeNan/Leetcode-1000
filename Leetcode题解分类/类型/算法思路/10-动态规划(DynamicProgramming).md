### 一.斐波那契数列
### 二.矩阵路径
### 三.数组区间
53. Maximum Subarray (Easy)
### 四.分割整数

### 五.最长递增子序列
## 1.[LC300-Longest Increasing Subsequence]

#### 2.[LC646-Maximum Length of Pair Chain]
思路：
设dp[n]为以index=n元素结尾的最长数对链的长度，则$dp[n] = max(dp[i] | i<n&&pairs[i][1]<pairs[n][1]);dp$数组的最大值就是结果
先对数组预处理，按照pair的第一个元素或者第二个元素排序
#### 3.[LC376-Wiggle Subsequence]
描述：如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为摆动序列，子序列是指从原序列中删除某些元素后剩下的元素组成的序列，要求保持剩下的元素在nums中的相对位置不变，
求所给序列的最长连续摆动子序列       
思路：  
(1)动态规划  
定义：  
up[n]为index范围[0~n]中以某一个元素结尾的最长上升摆动子序列  
down[n]为index范围[0~n]中以某一个元素结尾的最长下降摆动子序列  
转移方程：  
![](..\\pictures\\longest-wiggle-subsequence-4.png)  
(2)动态规划优化  
后一个状态只需要前一个状态来转移即可，比如求up[i]只需要up[i-1]或者down[i-1]，down[i]同理，所以可用两个变量up,down代替两个数组
所以最长摆动子序列总结为："n-1到n上升则更新上升变量up，n到n-1下降就更新下降变量down
```
    if(nums[i]<nums[i-1]){
        down = Math.max(down, up+1);
    }else if(nums[i]>nums[i-1]){
        up = Math.max(up, down+1);
    }
```
## 3.[最长数对链]
### 六.最长公共子序列
### 七.0/1背包
### 八.完全背包
### 九.二维费用的背包
### 十.多重背包
### 十一.物品带顺序的背包（排列）和不带顺序（组合）


###长度
w+1
### 初始化
没有选择任何一个背包中的元素时，对于1~N的dp值的意义一般是明确的，但是对于dp[0]的意义往往容易迷惑  
例子:  
(1)LC416. Partition Equal Subset Sum  
可以根据后面的dp主循环中，要得到dp[0]的操作来看其含义，比如背包当前容量为6，正在遍历背包中的数字6，选择了这个数字就得到dp[0]，  
而题目要求是否存在一种背包中元素的组合使得等于目标值，那么自然dp[0]意义就是true  
(2)LC494. Target Sum  
和上面类似的分析去看dp[0]的意义  
(3)LC474. Ones and Zeroes  
## 八.股票交易
## 通解
参考：https://leetCode-cn.com/circle/article/qiAgHn/
参考：https://leetCode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems
### 描述
给一个价格数组prices[]，index=i表示第i天的股票价格为prices[i]，每天最多只能执行一个买或卖的操作，给定最多进行k手交易（一手交易包括一次买和一次卖），求能获得的最大收益，一个人最多同时只能持有一个股票
### 递推方程
T[i][k]表示第i天结束时，在第0~i天最多进行k手交易后可以得到的最大收益，与T[i][k]相关的子问题有T[i-1][k],T[i-1][k-1],T[i]][k-1]，如何得到递推方程/转移方程  
因为一个人买入一个股票前，必须这个人当前持有的股票为0，卖出一个股票前必须当前持有的股票数量为1，所以可以根据第i天可以执行的操作：buy/sell/rest来讨论  
T[i][k][1] = max(T[i-1][k][1], T[i-1][k-1][0] - prices[i])  
T[i][k][0] = max(T[i-1][k][0], T[i-k][k][1] + prices[Ti])

## 特殊case
### k=1，只能进行一手交易
T[i][1][1] = max(T[i-1][1][1], T[i-1][0][0] - prices[i])
T[i][1][0] = max(T[i-1][1][0], T[i-1][1][1] + prices[i])
### k=2，可以进行多手交易
### k=+Infinity(可以进行无数手交易)
### k为任意值
### k=+Infinity且有冷却期
### k=+Infinity且交易费用
## 121. Best Time to Buy and Sell Stock( k=1 )
### 九.字符串编辑
#### leetCode-53. Maximum Subarray (Easy)
#### leetCode-392. Is Subsequence (Medium)
>动态规划判断是否子序列,对于海量输入降低处理时间

#### 树型DP
参考:https://leetcode-cn.com/problems/house-robber-iii/solution/shu-xing-dp-ru-men-wen-ti-by-liweiwei1419/

leetcode-337.打家劫舍 III  
leetcode-124.二叉树中的最大路径和  
leetcode-543.二叉树的直径  
leetcode-298.二叉树最长连续序列  
leetcode-549.二叉树中最长的连续序列  
leetcode-687.最长同值路径  
leetcode-1372.二叉树中的最长交错路径  
leetcode-865.具有所有最深节点的最小子树  