## 一.在基本有序的数组中查找
#### (1)Leetcode-33
>无重复元素

题目描述：升序排列的整数数组 nums 在预先未知的某个点上进行了旋转（例如， [0,1,2,4,5,6,7] 经旋转后可能变为 [4,5,6,7,0,1,2] ）。
请你在数组中搜索 target, 如果数组中存在这个目标值，则返回它的索引，否则返回-1
例1：
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1
例2：
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4
思路：对旋转数组，根据mid和left、right值得的对比可以得到[left, mid]有序或者[mid, right]有序，然后根据target是否在有序的部分数组区间可以缩小区间  
(1)判断$target == nums[mid]$,若是则返回mid，不是转向2
(2)若$nums[left]<=nums[mid]$为true(注意一定要<=)，则[left,mid]为有序区间，则判断$nums[left]<=target && target<nums[right]$为true则right = mid-1，为false则left = mid+1;  
若$nums[left]<=nums[mid]$为false,则[mid,right]为有序区间, 则判断$nums[mid]<target$&&$target<=nums[right]$，若为true则left = mid+1,为false则right = mid-1

#### (2)Leetcode-81
>可能有重复元素，则可能出现nums[mid]==nums[low]==nums[high]的情况，比如[1,0,1,1,1]，你无法分清楚哪个区间是有序的，所以直接low++，这样线性缩减
>若重复元素过多则导致事件复杂度趋向于O(N)

题目描述：按照升序排序的数组在预先未知的某个点上进行了旋转，判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false，可能包含重复元素。
#### (3)Leetcode-153
题目描述：假设按照升序排序的数组在预先未知的某个点上进行了旋转。例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2],请找出其中最小的元素。
>先找有序的那部分数组，所以循环结束条件为$left<rightnums[mid]<target && target<=nums[right]nums[mid]<target && target<=nums[right]$,判断其是在较大值部分，还是在较小值部分，已知nums[right]一定是较小值部分,数组无重复元素  
一个元素肯定是最小元素，这种题要用各种case来测试自己的代码，特别是[0],[0,1]这种极端情况
若[left,mid]为有序部分数组且$nums[mid]>nums[right]$则[left,mid]为较大值部分的有序数组，则最小值在[mid+1,right]  
若[left,mid]为有序部分数组且$nums[mid]<nums[right]$则[left,mid]为较小值部分的有序数组，则最小值在[left,mid]  
若[mid,right]为有序部分数组，则[mid,right]肯定是较小值部分数组，则最小值在[left, mid]之间  
考虑极端情况，mid,right都指向了最小值，则left++，所以最后right指向最小值
#### (4)Leetcode-154
题目描述：假设按照升序排序的数组在预先未知的某个点上进行了旋转，请找出其中最小的元素，可能存在重复的元素。
>参考81,当$nums[mid]==nums[low]==nums[high]$时，left++ 
>参考153，找最小元素
#### (5)Leetcode-162
>当$nums[mid]>nums[mid-1]$时,[mid,right]一定存在峰值,$nums[mid]<nums[mid-1]$时,[left, mid-1]一定存在峰值,所以可以缩小搜索范围，使用的是排除法，最后left==right时为解
>二分的思想是每次可以缩减一半的搜索空间,下面是我的一个解法，但并不是二分的思想，其实还是暴力，最坏时间度为O(N)
```
    // 存在返回index，不存在返回-1
    // 如果mid不是峰值，但是mid可以作为峰值的左边值或右边值
    // 题目给了任意两个数满足nums[i]!=nums[i+1]
    public int findPeakElement(int[] nums, int left, int right){
        // 区间长度小于2没有峰值
        if(right-left<2){
            return -1;
        }
        int mid = left + (right-left)/2;
        if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]){
            return mid;
        }
        // 如果mid不是峰值，但是mid可以作为峰值的左边值或右边值
        int leftIndex = findPeakElement(nums,left,mid);
        return leftIndex!=-1?leftIndex:findPeakElement(nums,mid,right);
    }
```

>二分的真谛是每次缩减一半空间
#### (6)Leetcode-852

## 二.最大值最小化问题
#### (1)Leetcode-410
#### (2)Leetcode-875
#### (3)Leetcode-1011
#### (4)Leetcode-1283
