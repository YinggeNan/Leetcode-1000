### <a id="_link_click_group">LeetCode-二分查找(BinarySearch)-medium-题单</a>
##### [LeetCode-29.两数相除](#_id29)
##### [LeetCode-33.搜索旋转排序数组](#_id33)
##### [LeetCode-34.在排序数组中查找元素的第一个和最后一个位置](#_id34)
##### [LeetCode-50.Pow(x,n)](#_id50)
##### [LeetCode-74.搜索二维矩阵](#_id74)
##### [LeetCode-81.搜索旋转排序数组II](#_id81)
##### [LeetCode-153.寻找旋转排序数组中的最小值](#_id153)
##### [LeetCode-162.寻找峰值](#_id162)
##### [LeetCode-209.长度最小的子数组](#_id209)
##### [LeetCode-222.完全二叉树的节点个数](#_id222)
##### [LeetCode-230.二叉搜索树中第K小的元素](#_id230)
##### [LeetCode-240.搜索二维矩阵II](#_id240)
##### [LeetCode-275.H指数II](#_id275)
##### [LeetCode-287.寻找重复数](#_id287)
##### [LeetCode-300.最长递增子序列](#_id300)
##### [LeetCode-378.有序矩阵中第K小的元素](#_id378)
##### [LeetCode-436.寻找右区间](#_id436)
##### [LeetCode-454.四数相加I](#_id454)
##### [LeetCode-475.供暖器](#_id475)
##### [LeetCode-497.非重叠矩形中的随机点](#_id497)

### LeetCode-二分查找(BinarySearch)-medium-题解
##### <a id="_id29">[LeetCode-29.两数相除](#_link_click_group)</a>
题目描述:不使用乘法和除法得到dividend/divisor的商  


思路:
公式:divide = divisor*(2^n)   
将divisor不停倍增,寻找当前dividend情况下的最大2^n  
然后dividendNext = dividendNext  - divisor*(2^currentMaxN)  
继续得到dividendNext对divisor的商  
注意溢出:
Integer.MIN_VALUE乘-1没有对应的正数,将dividend和divisor全部改为负数来运算就不会溢出了.
divisor自增过程中可能会溢出, 溢出后就不再是负数了.  
```
    // divide = divisor*(2^n), 时间复杂度O(logN)
    // 比如didivide为10, divisor为3, 10比3大,结果至少为1,3自增一倍为6, 10比6大,结果至少为2,6自增一倍为12,10小于12
    // 所以10减去其3最大的2的倍数6为4,判断4除3的商+2就是10除以3的商->递归产生了
    // 参考:https://leetcode-cn.com/problems/divide-two-integers/solution/po-su-de-xiang-fa-mei-you-wei-yun-suan-mei-you-yi-/

    // 将dividend和divisor全部改为负数运算,就不会溢出
    public int divide(int dividend, int divisor) {
        boolean flag = false;
        if(dividend == 0){
            return 0;
        }
        if(divisor == 1){
            return dividend;
        }
        if(divisor == -1){
            if(dividend == Integer.MIN_VALUE){
                return Integer.MAX_VALUE;
            }
            return -dividend;
        }
        // 题目规定不能用乘法,而且乘法会导致溢出, dividend*divisor<0
        if((dividend<0 && divisor>0) || (dividend>0 && divisor<0)){
            flag = true;
        }
        // 输入可能是-1,-1这种,必须将输入全部转化为负数
        dividend = dividend<0?dividend:(-dividend);
        divisor = divisor<0?divisor:(-divisor);
        if(dividend>divisor){
            return 0;
        }
        int res = div(dividend, divisor);
        return flag?-res:res;
    }
    // 用long型存储 dividend 和 divisor
    // divisor一直倍增,会导致int型溢出,用负数就不会有Intefer.MIN_VALUE溢出问题
    public int div(int dividend, int divisor){
        if(dividend > divisor){
            return 0;
        }
        int res = 1;
        int temp = divisor;
        // 溢出后temp不再小于0
        while(temp+temp < 0 && dividend<=temp+temp){
            res += res;
            temp += temp;
        }
        return res + div(dividend-temp, divisor);
    }
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
##### <a id="_id50">[LeetCode-50.Pow(x,n)](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id74">[LeetCode-74.搜索二维矩阵](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id81">[LeetCode-81.搜索旋转排序数组II](#_link_click_group)</a>
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
##### <a id="_id209">[LeetCode-209.长度最小的子数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id222">[LeetCode-222.完全二叉树的节点个数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id230">[LeetCode-230.二叉搜索树中第K小的元素](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id240">[LeetCode-240.搜索二维矩阵II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id275">[LeetCode-275.H指数II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id287">[LeetCode-287.寻找重复数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id300">[LeetCode-300.最长递增子序列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id378">[LeetCode-378.有序矩阵中第K小的元素](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id436">[LeetCode-436.寻找右区间](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id454">[LeetCode-454.四数相加I](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id475">[LeetCode-475.供暖器](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id497">[LeetCode-497.非重叠矩形中的随机点](#_link_click_group)</a>
题目描述:
思路:
```

```
