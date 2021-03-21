### <a id="_link_click_group">LeetCode-回溯(BackTracking)-medium-题单</a>
##### [LeetCode-17.电话号码的字母组合](#_id17)
##### [LeetCode-22.括号生成](#_id22)
##### [LeetCode-39.组合总和](#_id39)
##### [LeetCode-40.组合总和II](#_id40)
##### [LeetCode-46.全排列](#_id46)
##### [LeetCode-47.全排列II](#_id47)
##### [LeetCode-77.组合](#_id77)
##### [LeetCode-78.子集](#_id78)
##### [LeetCode-79.单词搜索](#_id79)
##### [LeetCode-89.格雷编码](#_id89)
##### [LeetCode-90.子集II](#_id90)
##### [LeetCode-93.复原IP地址](#_id93)
##### [LeetCode-211.添加与搜索单词-数据结构设计](#_id211)
##### [LeetCode-216.组合总和III](#_id216)
##### [LeetCode-254.因子的组合](#_id254)
##### [LeetCode-267.回文排列II](#_id267)
##### [LeetCode-291.单词规律II](#_id291)
##### [LeetCode-294.翻转游戏II](#_id294)
##### [LeetCode-306.累加数](#_id306)
##### [LeetCode-320.列举单词的全部缩写](#_id320)
##### [LeetCode-351.安卓系统手势解锁](#_id351)
##### [LeetCode-357.计算各个位数不同的数字个数](#_id357)
##### [LeetCode-491.递增子序列](#_id491)
##### [LeetCode-526.优美的排列](#_id526)
##### [LeetCode-784.字母大小写全排列](#_id784)
##### [LeetCode-797.所有可能的路径](#_id797)

### LeetCode-回溯(BackTracking)-medium-题解
##### <a id="_id17">[LeetCode-17.电话号码的字母组合](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id22">[LeetCode-22.括号生成](#_link_click_group)</a>
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
##### <a id="_id46">[LeetCode-46.全排列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id47">[LeetCode-47.全排列II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id77">[LeetCode-77.组合](#_link_click_group)</a>
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
##### <a id="_id89">[LeetCode-89.格雷编码](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id90">[LeetCode-90.子集II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id93">[LeetCode-93.复原IP地址](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id211">[LeetCode-211.添加与搜索单词-数据结构设计](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id216">[LeetCode-216.组合总和III](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id254">[LeetCode-254.因子的组合](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id267">[LeetCode-267.回文排列II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id291">[LeetCode-291.单词规律II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id294">[LeetCode-294.翻转游戏II](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id306">[LeetCode-306.累加数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id320">[LeetCode-320.列举单词的全部缩写](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id351">[LeetCode-351.安卓系统手势解锁](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id357">[LeetCode-357.计算各个位数不同的数字个数](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id357">[LeetCode-491.递增子序列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id491">[LeetCode-491. 递增子序列](#_link_click_group)</a>
题目描述:
思路:
```
    // 正确答案
    // 组合的一种,回溯即可
    // 不能对数组排序...
    public List<List<Integer>> findSubsequences(int[] nums) {
        if(nums==null || nums.length<2){
            return new ArrayList<>();
        }
        List<List<Integer>> res = new ArrayList<>();
        findSubsequences(nums, 0, res, new ArrayList<>());
        return res;
    }
    // index是输入序列的第index位置,考虑其是否加入临时结果集
    public void findSubsequences(int[] nums, int index, List<List<Integer>> res, List<Integer> current){
        if(index==nums.length && current.size()>1){
            res.add(new ArrayList<>(current));
        }
        if(index==nums.length){
            return;
        }
        int len = current.size();
        // 如果上一个选择的元素小于等于当前元素,则当前元素可以选择
        if(len==0 || (len>0 && current.get(len-1)<=nums[index])){
            current.add(nums[index]);
            findSubsequences(nums, index+1, res, current);
            current.remove(current.size()-1);
        }
        // 如果上一个选择的元素等于当前元素,则当前元素必须选择  
        // 所以只有当前元素不等于上一个元素时,当前元素才可以不选择   
        if(len==0 || (len>0 && current.get(len-1)!=nums[index])){
            findSubsequences(nums, index+1, res, current);
        }
    }
```
这个题非常重要,对比循环递归回溯和非循环递归回溯的区别:  
```
    // 下面的解法对于leetcode-491来说是错的,不过我这里是分析循环递归回溯的特点
    // index的含义
    // 假设结果集是最多n个数字的序列,那么index就代表结果集第index个位置的序列
    public void findSubsequences(int[] nums, int index, List<List<Integer>> res, List<Integer> current){
        res.add(new ArrayList<>(current));
        for(int i=index;i<nums.length;i++){
            // 对于重复的数,结果集的上一个选择的元素和当前元素相同时,当前元素必须选择
            // 比如对于4,6,7,7,上一个选择的元素为7(数组下标为2时),当前元素为7(数组下标为3时),
            // 当前元素必须选择
            current.add(nums[i]);
            findSubsequences(nums, i+1, res, current);
            current.remove(current.size()-1);
        }
    }
```
(1)适用于组合?排列?
非循环递归只适合组合问题  
循环递归适合排列问题,也适合大量组合问题  
(2)如何去重?
对于可以排序的输入来说: 优先选择循环递归,只选择重复元素序列中的第一个元素  
对于不能排序的输入而要去重(leetcode-491问题),采用非循环递归:  
规则就是如果前一个被选择的元素和当前考虑的元素相同时,当前元素必须选择.  
这个规则对于循环递归来说很难表示.因为循环递归是依靠for循环的下一次迭代来达到不选择上一个元素的：
leetcode-491这种题目很少见,背一波就好了   
去重一般还是使用循环递归   
```
  // 循环递归的这部分代码,是不可分割的，必须一起出现
  // 无法在循环递归里表示当前元素一定选择.  
  current.add(nums[i]);
  findSubsequences(nums, i+1, res, current);
  current.remove(current.size()-1);
```
(3)何时将临时结果加入全局结果  
非循环递归
递归深度到nums.length,从组合树来看就是到树的最底层时才开始将临时结果加入全局结果集   
循环递归
循环递归是在针对结果集的大小而言,每一层都是将临时结果集加入全局结果集  
(4)循环递归和非循环递归怎么表示考虑当前输入序列的i位置加入或者不加入临时结果集?  
循环递归只需要使用下面的代码,依靠循环迭代到下一个位置就实现当前位置元素加入和不加入临时结果集  
```
  // 循环递归的这部分代码,是不可分割的，必须一起出现
  // 无法在循环递归里表示当前元素一定选择.  
  current.add(nums[i]);
  findSubsequences(nums, i+1, res, current);
  current.remove(current.size()-1);
```
非循环递归要显示的调用两次递归函数
```
    // 当前元素加入结果集  
    current.add(nums[index]);
    findSubsequences(nums, index+1, res, current);
    current.remove(current.size()-1);
    // 当前元素不加入结果集    
    findSubsequences(nums, index+1, res, current);
```
(5)非循环递归函数和循环递归函数的参数index的意义   
非循环递归的index是考虑输入序列的index下标位置是否加入临时结果集    
循环递归的index是考虑临时结果集的第index下标位置是输入的哪个元素  
##### <a id="_id526">[LeetCode-526.优美的排列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id784">[LeetCode-784.字母大小写全排列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id797">[LeetCode-797.所有可能的路径](#_link_click_group)</a>
题目描述:
思路:
```

```
