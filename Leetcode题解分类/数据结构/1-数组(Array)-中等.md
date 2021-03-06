### <a id="_link_click_group">leetcode数组中等题单:</a>
##### [leetCode-11.盛最多水的容器](#_id11)
##### [leetCode-15.三数之和](#_id15)  
##### [leetCode-16.最接近的三数之和](#_id16)  
##### [leetCode-18.四数之和](#_id18) 
##### [leetCode-31.下一个排列](#_id31)  
##### [leetCode-33.搜索旋转排序数组 ](#_id33)
##### [leetCode-34.在排序数组中查找元素的第一个和最后一个位置](#_id34)
##### [leetCode-39.组合总和](#_id39)
##### [leetCode-40 组合总和 II](#_id40) 
##### [leetCode-48.旋转图像](#_id48)
##### [leetCode-54.螺旋矩阵](#_id54)
##### [leetCode-55.跳跃游戏](#_id55) 
##### [leetCode-56.合并区间](#_id56)
##### [leetCode-57.插入区间](#_id57)
##### [leetCode-59.螺旋矩阵 II](#_id59)

### leetcdoe数组中等题解:
#### <a id="_id11">[leetCode-11.盛最多水的容器](#_link_click_group)</a>
思路:双指针left,right左右夹逼法,当height[left]<=height[right]时,向里移动值较小的指针left  
[消去状态证明](https://leetCode-cn.com/problems/container-with-most-water/solution/shuang-zhi-zhen-fa-zheng-que-xing-zheng-ming-by-r3/)  
原理:双指针左右夹逼法将原本暴力迭代的O(N*N)的时间复杂度降低到O(N)的原理是每次移动一次指针都消去了搜索空间的一行或者一列   
相关题目有:  
leetCode-11 盛最多水的容器   
leetCode-167 两数之和 II - 输入有序数组  
设定1:
leetCode-167, 消去的搜索空间是nums[left]+nums[right]的和不等于target的index组合  
leetCode-11, 消去的搜索空间是已经计算过的容量或者小于已经计算过的容量的index组合  
问题1:初始化left=0,right=n-1,然后根据具体题目的规则比如leetCode-1的两数之和或者leetCode-11的乘积来移动指针，当left、high相遇时就停止，就考虑了所有的搜索空间并得到解了吗      
证明: 是的, 从left=0，right=n-1开始, 移动指针, 当left、right相遇后,就已经考虑过解空间的所有组合了.  
搜索空间如果用一个坐标系来看, leetCode-11和leetCode-167都是一个三角形,每次根据判断移动left或right指针后都会消去一行或一列搜索空间，最后当left、right相遇时，已经消去了所有的搜索空间了  
[搜索空间消去证明参考](https://leetCode-cn.com/problems/two-sum-ii-input-array-is-sorted/solution/yi-zhang-tu-gao-su-ni-on-de-shuang-zhi-zhen-jie-fa/)  

#### <a id="_id15">[leetCode-15.三数之和](#_link_click_group)</a>
#### <a id="_id16">[leetCode-16.最接近的三数之和](#_link_click_group)</a>
#### <a id="_id18">[leetCode-18.四数之和](#_link_click_group)</a>
#### <a id="_id31">[leetCode-31.下一个排列](#_link_click_group)</a>
#### <a id="_id33">[leetCode-33.搜索旋转排序数组](#_link_click_group)</a>
#### <a id="_id34">[leetCode-34.在排序数组中查找元素的第一个和最后一个位置](#_link_click_group)</a>
#### <a id="_id39">[leetCode-39.组合总和](#_link_click_group)</a>
思路:先思考对数组如何得到排列和组合的情况，比如给一个数组[a1,a2,a3,a4,a5]  
(1)全排列: 求给所有数组元素的所有排列情况,每个排列中每个元素用一次,每个排列必须包含所有元素  
(2)所有的排列:求给所有数组元素的所有排列情况,每个排列中每个元素用一次  
(4)组合:所给数组无重复值,求给所有数组元素的所有组合情况,每个排列中每个元素可用无数次,结果集合中不能包含重复值  
(4)组合:所给数组有可能有重复值,求给所有数组元素的所有组合情况,每个排列中每个元素可用一次,结果集合中不能包含重复值  
#### <a id="_id40">[leetCode-40.组合总和 II](#_link_click_group)</a> 
#### <a id="_id48">[leetCode-48.旋转图像](#_link_click_group)</a>
#### <a id="_id54">[leetCode-54.螺旋矩阵](#_link_click_group)</a>
#### <a id="_id55">[leetCode-55.跳跃游戏](#_link_click_group)</a>
#### <a id="_id56">[leetCode-56.合并区间](#_link_click_group)</a>
#### <a id="_id57">[leetCode-57.插入区间](#_link_click_group)</a>
```
    // 插入和区间和原区间列表中所有重叠的区间合并为一个大区间,然后加上区间列表中不重叠的区间即可
    // left = newInterval[0];right = newInterval[1]
    // 遍历intervals的区间(l,r),若r<left说明(l,r)在newInterval的左边直接加入
    // 若l>right,则说明(l,r)在newInterval的右边,直接加入
    // 否则说明区间和newInterval有重叠,更新重叠区域的left和right
    // 插入newInterval的时机是扫描到第一个l>right的区间.
    // 不要尝试先找到intervals中的重叠区间的最左区间和最右区间位置,然后将所有重叠区间融合为一个
    // 因为可能没有重叠区间,这样你还需要判断是否存在融合区间
    // 重叠区间的融合结果是并集: left = Math.min(left, l), right = Math.max(right, r)
    public int[][] insert(int[][] intervals, int[] newInterval) {
        boolean used = false;
        int left = newInterval[0], right = newInterval[1];
        List<int[]> res = new ArrayList<>();
        for(int[] num: intervals){
            if(num[1]<left){
                res.add(num);
            }else if(num[0]>right){
                if(!used){
                    res.add(new int[]{left, right});
                    used = true;
                }
                res.add(num);
            }else{
                left = Math.min(left, num[0]);
                right = Math.max(right, num[1]);
            }
        }
        // 如果intervals中没有在newInterval右边的区间
        if(!used){
            res.add(new int[]{left, right});
        }
        return res.toArray(new int[res.size()][]);
    }
```
#### <a id="_id59">[leetCode-59.螺旋矩阵 II](#_link_click_group)</a>