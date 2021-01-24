1-maximum sum subarray of size k-easy
2-smallest subarray with a given sum-easy
3-longest substring with k distinct characters-medium
4-fruits into baskets-medium
5-no-repeat substring-hard
6-longest substring with same letters after replacement -hard
7-longest subarray with ones after replacement-hard
#### leetcode-3.[Longest Substring Without Repeating Characters]
>连续字符的字串可以考虑滑动窗口  
>双指针+滑动窗口

题目：给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。  
思路：判断有无重复元素用map {value:index}，无重复元素的子串用left,right两个指针来限定范围。  
遇到重复元素时对窗口左边界的处理: left = Math.max(left, map.get(str[right]))  
  (1)比如abca,初始化left=0，right=3时str[left]和str[right]都是a，表示本轮无重复元素结束, 且index从[left+1,right)开始的所有字串长度都小于index=0开始的字串，left应该直接直接置为right，置maxLength = Math.max(maxLength, right-left)  
  (2)而abcafb，left从3开始，right=5时，map的key有a,b,c,f, str[right]在map中存在了，但是此时left>1，之前的b不在当前窗口中，所以不需要把当前窗口截断  
#### leetcode-76.[Minimum Window Substring](https://leetcode-cn.com/problems/minimum-window-substring/)
题目描述：给字符串s,字符串t,返回s中涵盖t所有字符的最小子串。如果s中不存在涵盖 所有字符的子串，则返回空字符串""  
例子：  
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC" 
思路：  
1.left,right初始化为0，设置need,window两个map，用来保存字符频数{char:count}
2.right右移动找到可行解  
3.left左移动找到本次可行解的最优解  
4.重复2，3步骤找到所有可行解的最优解，得到全局最优解
[参考代码](https://leetcode-cn.com/submissions/detail/140923136/)  
[参考](https://leetcode-cn.com/problems/minimum-window-substring/solution/76-zui-xiao-fu-gai-zi-chuan-hua-dong-chu-9ju0/)
#### leetcode-209
思路类似leetcode76
#### leetcode-424
[参考](https://leetcode-cn.com/problems/longest-repeating-character-replacement/solution/tan-xin-de-hua-dong-chuang-kou-si-lu-qing-xi-dai-m/)
#### leetcode-438
#### leetcode-567
#### leetcode-713
#### leetcode-763
#### leetcode-845
#### leetcode-881
#### leetcode-904
#### leetcode-978
#### leetcode-992
#### leetcode-1004
#### leetcode-1040
#### leetcode-1052