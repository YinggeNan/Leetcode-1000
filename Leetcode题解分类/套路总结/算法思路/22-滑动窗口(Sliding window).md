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
参考：https://leetcode-cn.com/problems/minimum-window-substring/solution/76-zui-xiao-fu-gai-zi-chuan-hua-dong-chu-9ju0/


第 209 题
第 424 题
第 438 题
第 567 题
第 713 题
第 763 题
第 845 题
第 881 题
第 904 题
第 978 题
第 992 题
第 1004 题
第 1040 题
第 1052 题
#### leetcode-424
