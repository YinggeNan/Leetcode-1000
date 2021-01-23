#### Move Zeroes-easy  
题目描述: 把数组中的 0 移到末尾
思路: 重插入数组

#### Reshape the Matrix-easy
思路: 重插入二维数组

#### Max Consecutive Ones-easy

题目描述: 找出数组中最长的连续 1
思路: 设置两个变量，全局连续1 globalAcount、单次扫描连续1 partialCount，
遍历数组，遇到1则partialCount加1，遇到0则设置globalAcount为max(globalAcount为max, partialCount)，
且partialCount重置为0

#### Search a 2D Matrix II -easy

对于每行从左到右升序，每列从上到下升序的matrix，
查找某个元素，从右上角元素x开始，x>target则转向x的left，
x<target则转向x的down

#### Find the Duplicate Number-Medium

题目描述: n+1个数放到长度为n的数组里，且每个数取值范围1~n,只有一个重复数字,求重复数字
思路:
快慢指针：对于这种将集合S中的所有元素映射到自身集合S的问题，可以用tortiose and hare algorithm算法
输入数组为nums，将其一个index看作一个节点，则其所有index的指向关系构成了一个循环链表，
fast指针步长为2(nums[nums[fast])，slow指针步长为1(nums[slow]
第一个循环找相遇点：初始为fast=nums[nums[0]], slow=nums[0]，fast步长2，slow步长1出发，相遇于x
第二个循环找重复元素(cycle开始节点)：fast从x，slow从0开始都以步长为1继续出发，最后相遇于重复元素值


二分搜索：value range搜索，对[1,n]进行搜索，设low=1, high = n+1(为了mid能为n), mid=low+(high-low)/2;
统计数组里小于等于mid(为什么有小于的情况，因为可能数组的所有数都为同一个值)的数count，如果count<mid，
则说明重复的数在[mid+1,high]之间则low = mid+1;如果count>mid，说明重复的数在[low,mid]之间则high=mid
最后low和high会相遇于mid

#### Set Mismatch-Easy

题目描述: 
将1~n这n个数字放到长为n的数组nums中，将其中一个数字x从其位置上删除，
并放置了一个1~n的非x的其他数字，也就是说有一个重复数字
思路:
排序解法：设数组为nums，长L，排序数组，然后从0开始遍历数组，对比i和i+1位置的数，检测到重复后，
将从i+1到L-1位置的所有元素左移一位，然后再次遍历整个数组，当nums[i]!=i+1时，i+1就是missing元素

交换解法：核心思想就是将值为x的值元素放到x-1的位置上，扫描数组，判断当前位置i上的值nums[i]是否为i+1，
如果是，则继续判断下一个位置，如果不是，则将nums[i]放到其正确的位置num[i]-1上，放之前也要判断位置上nums[i]-1
是否有值，若有值则继续判断下一个位置，没有则交换i和nums[i]-1的位置，交换后继续判断当前位置i上的值是否满足
条件，循环处理直到不当前位置有正确的值或要放的位置已经有正确值为止

#### Beautiful Arrangement

题目描述: 有一个set包含了从1~N的所有元素，要得到这样的序列，index为i上的元素value满足
index能被value整除或者value能被index整除，求所有这样的序列的数量，index从1开始
思路: DFS + 回溯; 状态数组的使用; 递归出口如何定义,这里只需要求符合条件的序列的数量，所有不需要返回真正的序列
递归函数定义一个参数pos,表示本次调用是放置pos位置的值，隐含表示1~(pos-1)都找好了，所以pos为N+1时表示找到一个符合
条件的序列
code: https://leetcode.com/submissions/detail/435610590/

#### Permutations

题目描述: 全排列
思路: DFS + 回溯；状态数组的使用(本题也可以不使用状态数组，看一个元素有没有使用过直接搜索currentPermutation也行
不过这样时间复杂度为O(N); currentPermutation最后加入globalPermutation时要放置currentPermutation的copy
递归出口是currentPermutation的长度为输入数组的长度
参考: https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)

#### Degree of an Array (Easy)

题目描述: 找到给定数组的一个子数组(必须是从原数组连续元素截取)的最高频率和原数组一致，该子数组长度最小
思路: 找到所有可能的最大频率的元素，计算这些元素的lastPos-firstPos+1的最小值
Code: https://leetcode.com/submissions/detail/435633431/
进阶: 一次遍历解决,用一个countMap来统计每个元素出现的频率，用一个firstMap来记录每个元素第一次出现的位置，
degree变量表示当前频率最大值，minLength表示所求最小连续子数组长度，遍历数组，对于每个当前遍历的元素x
如果x的频率大于degree，则更新degree并赋值minLenghth为currentPosOfx-firstPosOfx+1，如果其频率等于degree，
则minLenghth = math.min(minLenghth, currentPosOfx-firstPosOfx+1)
参考: https://leetcode.com/problems/degree-of-an-array/discuss/124317/JavaC%2B%2BPython-One-Pass-Solution
#### Toeplitz Matrix-Easy
题目描述: 如果矩阵上每一条由左上到右下的对角线上的元素都相同，那么这个矩阵是 托普利茨矩阵
思路:
(1)解法1:遍历第一排和第一列的每个元素，遍历到一个元素a，坐标为(x,y)时，就一直沿着其右下方对角线遍历，既x++,y++，
检测是否对角线上的元素一样，这样需要检测是否越界
(2)解法2:遍历row range [0,matrix.length-1], column range [0,matrix[0].length-1]的每个元素a，坐标为(x,y)，检测
其matrix[x][y]是否等于matrix[x+1][y+1]即可，比解法1简洁很多

#### Array Nesting-Medium

题目描述: https://leetcode-cn.com/problems/array-nesting/
思路:可以证明任给一个index=x开始，比如x=1，然后得到index=1上的值A[x]，
用A(x)作为index继续寻找，最后会找到一个index=y，a[y]必然等于x，
既上述的index必然形成一个环，而A[index]就是指引环中一个节点index到另一个节点index的方向
所有0到N-1的这N个index可以分为好几组，每一组都形成一个环，且每一组的环都和别的组的环不相交，题目要求的
就是这些环中的最大环长度，所以我们遍历任意一个元素都只需要遍历一遍，因为这个元素只属于一个环，
所以一个index被遍历后就标记这个index，比如可以设置A[index]为-1，当遍历到一个A[x]为-1时直接i跳过即可
#### Max Chunks To Make Sorted-Medium
题目描述: 数组arr是[0, 1, ..., arr.length - 1]的一种排列，我们将这个数组分割成几个“块”，
并将这些块分别进行排序。之后再连接起来，使得连接的结果和按升序排序后的原数组相同
思路: 设一个当前index=i的最大值indexMax，为从index=0开始到当前位置index=i的最大值，如果
indexMax等于i则可以划分的块加1
#### Two Sum (Easy)
题目描述: 数组中两个数的和为给定值
思路:
(1)双指针-顺序查找
(1)双指针-二分查找？如何实现
(3)map
#### Contains Duplicate (Easy)
题目描述: 判断数组是否含有重复元素
思路: set
(1)后面遍历的元素是否已经在set中存在
(2)利用set去重，把所有元素加入set，最后判断set长度是否等于数组长度
#### Longest Harmonious Subsequence (Easy)
题目描述: 给一个数组，求其最长差值为1的子序列的长度
思路: 得到每个元素num的num+1或num-1的数量，为什么num+1或num-1都可以，
因为是对数组所有元素遍历，所有num+1或num-1都能得到所有情况
(1)暴力遍历每个元素num，统计num和num+1的频率
(2)hash表，存储每个元素的频率