## 滑动窗口题眼-连续字符的子串
#### leetcode-3.[Longest Substring Without Repeating Characters]
题目：给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。
>right指针遇到第一个窗口中有重复元素,新left=max.(left, map.get(left));

思路：判断有无重复元素用map {value:index}，无重复元素的子串用left,right两个指针来限定范围。  
遇到重复元素时对窗口左边界的处理: left = Math.max(left, map.get(str[right]))  
(1)比如abca,初始化left=0，right=3时str[left]和str[right]都是a，表示本轮无重复元素结束, 且index从[left+1,right)开始的所有字串长度都小于index=0开始的字串，left应该直接直接置为right，置maxLength = Math.max(maxLength, right-left)  
(2)而abcafb，left从3开始，right=5时，map的key有a,b,c,f, str[right]在map中存在了，但是此时left>1，之前的b不在当前窗口中，所以不需要把当前窗口截断  
#### leetcode-76.[Minimum Window Substring](https://leetcode-cn.com/problems/minimum-window-substring/)
题目描述：给字符串s,字符串t,返回s中涵盖t所有字符的最小子串。如果s中不存在涵盖 所有字符的子串，则返回
空字符串""  
>right右移找可能解(包含了所有字符既包含t的所有可能的key，且频数大于等于，但是可能有其他字符)，left移动找符合要求的解

例子：  
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC" 
思路：  
1.left,right初始化为0，设置need,window两个map，用来保存字符频数{char:count}
2.right不断右移找到可行解  
3.left左移动找到本次可行解的最优解并更新全局最优解，直到本轮可行解无解，继续2 
[参考代码](https://leetcode-cn.com/submissions/detail/140923136/)  
[参考](https://leetcode-cn.com/problems/minimum-window-substring/solution/76-zui-xiao-fu-gai-zi-chuan-hua-dong-chu-9ju0/)
#### leetcode-209
题目描述：给定一个含有n个正整数的数组和一个正整数s，找出该数组中满足其和≥s的长度最小的连续子数组，并返回其长度，若不存在符合条件的子数组，返回0
>right移动找可能解(包含了所有字符，但是可能有其他字符)，left移动找符合要求的解
> 思路类似leetcode76.[Minimum Size Subarray Sum](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)  

思路:  
0.left = 0, right = 0  
1.right右移动直到找到可行解  
3.left左移动找到本次可行解的最优解并更新全局最优解，直到本轮可行解无解，继续2 
#### leetcode-424.[Longest Repeating Character Replacement](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)
题目描述：给一个仅由大写英文字母组成的字符串，可将任意位置上的字符替换成另外的字符，可最多替换k次,找到包含重复字母的最长子串的长度
>窗口扩张+窗口滑动

思考：想要得到最长的重复字母子串，则对原字符串任取的一个子串来说，其除了最高频重复字母之外的其他字母最多有k个，所以如何计算一段子串中除了最高频之外的其他字符的数量是重点  
思路:  
0.left = 0, right = 0, maxRepeatedLength = 0;  
1.窗口扩充right++可行解，直到[left,right]之间无可行解，转向2
2.窗口滑动left++,right++左移使得[left,right]有可行解，转向1
```
    // 最佳代码
    public int characterReplacement(String s, int k) {
        int[] record = new int[26];
        int len = s.length();
        char[] arr = s.toCharArray();
        int left = 0;
        int right = 0;
        int historyMax = 0;
        while (right < len) {
            record[arr[right] - 'A']++;
            historyMax = Math.max(historyMax, record[arr[right] - 'A']);
            right++;
            while (right - left > historyMax + k) {
                record[arr[left] - 'A']--;
                left++;
            }
        }
        // 按照窗口扩充right++，窗口滑动left++,right++，则最大值是right-left+1,但是最后right的值会移动到s.length()超出范围
        // 所以最后实际有效right = right-1
        return right - left;
    }
```
[参考]https://leetcode-cn.com/problems/longest-repeating-character-replacement/solution/tong-guo-ci-ti-liao-jie-yi-xia-shi-yao-shi-hua-don/)
#### leetcode-438
题目描述：给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引，字符串只包含小写英文字母
>right移动找可能解(包含了所有字符，但是可能有其他字符)，left移动找符合要求的解(right-left-1==window.size())

例1：  
输入:  
s: "cbaebabacd" p: "abc"  
输出:  
[0, 6]  
解释:  
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。  
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。  
例2：    
输入:  
s: "abab" p: "ab"  
输出:  
[0, 1, 2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。  
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。  
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。  
#### leetcode-567
题目描述：给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。 
>right移动找可能解(包含了所有字符，但是可能有其他字符)，left移动找符合要求的解(s1.length()==window.size())

例1：   
输入: s1 = "ab" s2 = "eidbaooo"  
输出: True  
解释: s2 包含 s1 的排列之一 ("ba").  
例2：
输入: s1= "ab" s2 = "eidboaoo"  
输出: False  
#### leetcode-713
题目描述：给定一个正整数数组 nums，找出该数组内乘积小于 k 的连续的子数组的个数。
>right右移当窗口内乘积>=k时left右移找符合要求的解

输入: nums = [10,5,2,6], k = 100  
输出: 8  
解释: 8个乘积小于100的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。  
需要注意的是 [10,5,2] 并不是乘积小于100的子数组。  
#### leetcode-395
题目描述：找到给定字符串（由小写字符组成）中的最长子串 T ， 要求 T 中的每一字符出现次数都不少于 k 。输出 T 的长度

思路1-滑动窗口解法： 
右移动窗口，统计窗口中频数>=k的key个数validKey，然后右移动left，当window.size()==validkey时，窗口的子串符合要求，问题的难点在于right什么时候需要停下来右移动left，考虑只有小写字符，所以窗口中最多不同的数有26个，所以对上面程序片段循环考虑，考虑right在window.size()为[1,26]时停下，得到最大子串长度，O(N)  
[思路2](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/solution/26zi-fu-qian-zhui-he-fen-zhi-er-cha-shu-de-hou-xu-/)-前缀和+分治  
有点难理解
#### leetcode-763
题目描述：字符串 S 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一字母最多出现在一个片段中。返回一个表示每个字符串片段的长度的列表。

[贪心法](https://leetcode-cn.com/problems/partition-labels/solution/hua-fen-zi-mu-qu-jian-by-leetcode-solution/)
#### leetcode-30
>(1)word作为targetMap的key
>(2)left,right指针的初始位置范围是[0,word.length-1]

题目描述：给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置，注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。
例1：
输入：  
  s = "barfoothefoobarman",  
  words = ["foo","bar"]  
输出：[0,9]  
解释：  
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。  
输出的顺序不重要, [9,0] 也是有效答案。  
例2：  
输入：  
  s = "wordgoodgoodgoodbestword",  
  words = ["word","good","best","word"]  
输出：[]  
#### leetcode-845
#### leetcode-881
#### leetcode-904
#### leetcode-978
#### leetcode-992
#### leetcode-1004
#### leetcode-1040
#### leetcode-1052
