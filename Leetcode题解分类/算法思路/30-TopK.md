1-Top 'K' Numbers (easy)
2-Kth Smallest Number (easy)
3-'K' Closest Points to the Origin (easy)
4-Connect Ropes (easy)
5-Top 'K' Frequent Numbers (medium)
6-Frequency Sort (medium)
7-Kth Largest Number in a Stream (medium)
8-'K' Closest Numbers (medium)
9-Maximum Distinct Elements (medium)
10-Sum of Elements (medium)
11-Rearrange String (hard)
## Kth Smallest Element in a Sorted Matrix-Medium
```
题目描述: 一个矩阵，从上到下递增排序，从左到右递增排序，求矩阵中第k小的数
思路:
堆解法：最小堆，对于矩阵来说最小的数肯定在第一行中，那么第二小的数在哪里呢？设set有且仅有第一行的所有数，最小的数为x，
那么将x下方(第二行)的y加入到set中，此时set中最小的数就是第二小的数，同理循环k-1即可得到最小的数
```
```
二分搜索：因为是二维数组，所以不能是index range的二分搜索，只能是value range的二分搜索
核心思想就是找到一个数x(存在于矩阵中)，让矩阵中所有小于x的数有k-1个，那么x就是第k小的数了,设矩阵最大值为max，最小值为min
对[min,max]范围进行二分搜索，low=min，high=max+1(要让mid的值有为max的可能，所以low不能为max）\，
得mid=left+(right-left)/2, 遍历数组nums统计所有小于等于mid的数的个数count，若count<=k则说明low到mid之间不存在x，
则low=mid+1，若count>k则x就在low到mid之间，high=mid, 最后low 和high会相遇于x。
```