### <a id="_link_click_group">LeetCode-数组(array)-medium-题单</a>
##### [LeetCode-11.盛最多水的容器](#_id11)
##### [LeetCode-15.三数之和](#_id15)
##### [LeetCode-16.最接近的三数之和](#_id16)
##### [LeetCode-18.四数之和](#_id18)
##### [LeetCode-31.下一个排列](#_id31)
##### [LeetCode-33.搜索旋转排序数组](#_id33)
##### [LeetCode-34.在排序数组中查找元素的第一个和最后一个位置](#_id34)
##### [LeetCode-39.组合总和](#_id39)
##### [LeetCode-40.组合总和II](#_id40)
##### [LeetCode-48.旋转图像](#_id48)
##### [LeetCode-54.螺旋矩阵](#_id54)
##### [LeetCode-55.跳跃游戏](#_id55)
##### [LeetCode-56.合并区间](#_id56)
##### [LeetCode-57.插入区间](#_id57)
##### [LeetCode-59.螺旋矩阵II](#_id59)
##### [LeetCode-62.不同路径](#_id62)
##### [LeetCode-63.不同路径II](#_id63)
##### [LeetCode-64.最小路径和](#_id64)
##### [LeetCode-73.矩阵置零](#_id73)
##### [LeetCode-74.搜索二维矩阵](#_id74)
##### [LeetCode-75.颜色分类](#_id75)
##### [LeetCode-78.子集](#_id78)
##### [LeetCode-79.单词搜索](#_id79)
##### [LeetCode-80.删除排序数组中的重复项II](#_id80)
##### [LeetCode-81.搜索旋转排序数组II](#_id81)
##### [LeetCode-90.子集II](#_id90)
##### [LeetCode-105.从前序与中序遍历序列构造二叉树](#_id105)
##### [LeetCode-106.从中序与后序遍历序列构造二叉树](#_id106)
##### [LeetCode-120.三角形最小路径和](#_id120)
##### [LeetCode-152.乘积最大子数组](#_id152)
##### [LeetCode-153.寻找旋转排序数组中的最小值](#_id153)
##### [LeetCode-162.寻找峰值](#_id162)
##### [LeetCode-189.旋转数组](#_id189)
##### [LeetCode-209.长度最小的子数组](#_id209)
##### [LeetCode-216.组合总和III](#_id216)
##### [LeetCode-229.求众数II](#_id229)
##### [LeetCode-238.除自身以外数组的乘积](#_id238)
##### [LeetCode-245.最短单词距离III](#_id245)
##### [LeetCode-259.较小的三数之和](#_id259)
##### [LeetCode-277.搜寻名人](#_id277)
##### [LeetCode-280.摆动排序](#_id280)
##### [LeetCode-287.寻找重复数](#_id287)
##### [LeetCode-289.生命游戏](#_id289)
##### [LeetCode-370.区间加法](#_id370)
##### [LeetCode-380.常数时间插入、删除和获取随机元素](#_id380)
##### [LeetCode-442.数组中重复的数据](#_id442)
##### [LeetCode-457.环形数组是否存在循环](#_id457)
##### [LeetCode-495.提莫攻击](#_id495)

### LeetCode-数组(array)-medium-题解
##### <a id="_id11">[LeetCode-11.盛最多水的容器](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id15">[LeetCode-15.三数之和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id16">[LeetCode-16.最接近的三数之和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id18">[LeetCode-18.四数之和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id31">[LeetCode-31.下一个排列](#_link_click_group)</a>
题目描述:将给定数字序列重新排列成字典序中下一个更大的排列，如果不存在下一个更大的排列则将数字序列升序排列  
思路:从右往左找第一个顺序对,既index满足i<i+1 && nums[i]<nums[i+1],然后从右往左找第一个大于nums[i]的元素([i+1,n-1]为降序),设下标为k,则将nums[i]和nums[k]交换,然后将[i+1,n-1]升序排列(因为此时为逆序,所以双指针交换)
```

```
##### <a id="_id33">[LeetCode-33.搜索旋转排序数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id34">[LeetCode-34.在排序数组中查找元素的第一个和最后一个位置](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id39">[LeetCode-39.组合总和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id40">[LeetCode-40.组合总和II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id48">[LeetCode-48.旋转图像](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id54">[LeetCode-54.螺旋矩阵](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id55">[LeetCode-55.跳跃游戏](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id56">[LeetCode-56.合并区间](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id57">[LeetCode-57.插入区间](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id59">[LeetCode-59.螺旋矩阵II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id62">[LeetCode-62.不同路径](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id63">[LeetCode-63.不同路径II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id64">[LeetCode-64.最小路径和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id73">[LeetCode-73.矩阵置零](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id74">[LeetCode-74.搜索二维矩阵](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id75">[LeetCode-75.颜色分类](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id78">[LeetCode-78.子集](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id79">[LeetCode-79.单词搜索](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id80">[LeetCode-80.删除排序数组中的重复项II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id81">[LeetCode-81.搜索旋转排序数组II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id90">[LeetCode-90.子集II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id105">[LeetCode-105.从前序与中序遍历序列构造二叉树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id106">[LeetCode-106.从中序与后序遍历序列构造二叉树](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id120">[LeetCode-120.三角形最小路径和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id152">[LeetCode-152.乘积最大子数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id153">[LeetCode-153.寻找旋转排序数组中的最小值](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id162">[LeetCode-162.寻找峰值](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id189">[LeetCode-189.旋转数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id209">[LeetCode-209.长度最小的子数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id216">[LeetCode-216.组合总和III](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id229">[LeetCode-229.求众数II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id238">[LeetCode-238.除自身以外数组的乘积](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id245">[LeetCode-245.最短单词距离III](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id259">[LeetCode-259.较小的三数之和](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id277">[LeetCode-277.搜寻名人](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id280">[LeetCode-280.摆动排序](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id287">[LeetCode-287.寻找重复数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id289">[LeetCode-289.生命游戏](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id370">[LeetCode-370.区间加法](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id380">[LeetCode-380.常数时间插入、删除和获取随机元素](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id442">[LeetCode-442.数组中重复的数据](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id457">[LeetCode-457.环形数组是否存在循环](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id495">[LeetCode-495.提莫攻击](#_link_click_group)</a>
题目描述:
思路:
```

```
