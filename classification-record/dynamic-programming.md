# 一.斐波那契数列
# 二.矩阵路径
# 三.数组区间
# 四.分割整数

# 五.最长递增子序列
## 1.[LC300- Longest Increasing Subsequence](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

## 2.[LC646-Maximum Length of Pair Chain](https://leetcode-cn.com/problems/most-stones-removed-with-same-row-or-column/)
思路：
设dp[n]为以index=n元素结尾的最长数对链的长度，则dp[n] = max(dp[i] | i<n&&pairs[i][1]<pairs[n][1]);dp数组的最大值就是结果
先对数组预处理，按照pair的第一个元素或者第二个元素排序
## 2.[LC376-Wiggle Subsequence ](https://leetcode-cn.com/problems/most-stones-removed-with-same-row-or-column/)
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
# 六.最长公共子序列
#七.背包
# 八.股票交易
# 九.字符串编辑