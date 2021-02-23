#### leetcode-283.移动零
>原地重建数组

题目描述: 把数组中的所有0移到末尾 ，保持其他元素的相对位置不变  
思路: 扫描数组，index=0，元素大于0时插入在index位置且index++，设数组长为N，数组扫描完毕后将[index,N-1]区间赋值为0

#### leetcode-566.重塑矩阵
>原地重建二维数组 
思路: 重插入二维数组，对原二维数组的任意一个数的坐标(x,y)，计算其在新二维数组的新坐标(x1,y1)并插入    
如果把二维数组呈一维展开，设(x,y)为原数组的第k个数，如何计算k？  
(1)累加器count计数得到  
(2)公式计算k = x*c0+y+1;c0是原数组列宽度   
累加器比公式计算更简单，不需要重复做计算  
```
// 从原数组index->新数组index
x1 = (k-1)/c;     
y1 = (k-1)%c;
count++;
```

#### Leetcode-485.最大连续1的个数
> 统计最大连续的某个数

题目描述: 找出数组中最长的连续 1的长度
思路: 设置两个变量，全局连续1的最大值globalCount、单次扫描连续1的最大值partialCount  
遍历数组，遇到1则partialCount++，遇到0则globalCount=max(globalCount, partialCount)，且partialCount重置为0; 扫描完毕后令globalCount为max(globalCount, partialCount)

#### Leetcode-240.搜索二维矩阵 II
问题: 在一个M*N的矩阵中，每行元素从左到右递增，每列元素从上到下递增，给定一个值target，查找target是否存在于矩阵中  
思路: 从右上角元素x开始，x>target则转向x的左边的第一个元素，$x<target$则转向x的下方第一个元素，时间复杂度O(M+N);也可以从左下角元素开始

#### Leecode-287.寻找重复数
题目描述: n+1个数放到长度为n的数组里，且每个数取值范围1~n,只有一个重复数字,求这个重复数字, 要求用O(1)空间解法   
思路1-快慢指针：对于这种将集合S中的所有元素映射到自身集合S的问题，可以用tortoise and hare algorithm算法    
    输入数组为nums，将其一个index看作一个节点，则其所有index的指向关系构成了一个循环链表，  
    fast指针步长为2(nums[nums[fast])，slow指针步长为1(nums[slow]  
    第一个循环找相遇点：初始为fast=nums[nums[0]], slow=nums[0]，fast步长2，slow步长1出发，相遇于x  
    第二个循环找重复元素(cycle开始节点)：fast从x，slow从0开始都以步长为1继续出发，最后相遇于重复元素值
思路2-对index的二分搜索:  
排序后初始化low=0,high=n-1;  计算区间[low,mid]的长度length,统计数组在index位于[low,mid]的元素个数number   
如果$length<number$,说明重复数在[low,mid]之间,令high = mid,否则说明重复数在[mid,high]之间,令low = mid  
循环结束条件为$low<high-1$,既最后只剩两个元素时,low,high一定都是重复元素,返回low或high   
思路2-对value的二分搜索：  
对[1,n]进行搜索，设low=1, high = n+1(为了mid能为n)  
mid=low+(high-low)/2;统计数组里小于等于mid(为什么有小于的情况，因为可能数组的所有数都为同一个值)的数count，如果$count<mid$，则说明重复的数在[mid+1,high]之间则low = mid+1;如果count>mid，说明重复的数在[low,mid]之间则high=mid，最后low和high会相遇于mid

#### leetcode-73.矩阵置零
>空间复杂度O(1)的解法,先扫描第一行和第一列是否有0，重用第一行和第一列作为标志

#### leetcode-645.错误的集合
思想-统计法:统计每个数的频率,重复的那个数频率为2,缺失的那个数频率为1  
解法1:暴力解法,对范围[1,n]的数字, 遍历数组nums统计出现的次数,出现2次的为重复,出现0次的为缺失的,时间复杂度O(N*N)  
解法2:暴力优化,在解法1的基础上,找到了重复的和缺失的数就停止遍历,事件复杂度O(N*N)  
解法3:使用map存储{number:frequency},统计数组nums中所有元素出现的次数,再对范围[1,n]的数字,检查map里是否存在或者频率为2次,时间复杂度O(N),空间复杂度O(N)  
解法4:排序,设数组为nums,长为L,从0开始遍历数组，对比i和i+1位置的数，检测到重复后，将i+1到L-1位置的所有元素左移一位,然后再次遍历整个数组,当nums[i]!=i+1时，i+1就是missing元素  
解法5:使用数组存储number的frequency,数组的index作为number  
解法6:标记法,扫描数组nums,对每个已遍历过的数字都标记,当前遍历的值为value=nums[i],如果nums[value]>0,则设置nums[value-1]为-1,若nums[value]<0,则value就是重复的元素,最后扫描一遍数组,nums[i]>0时,i+1就是缺失的数字  
解法7:异或运算  

#### leetcode-526.优美的排列
思路: DFS + 回溯+状态数组的使用; 递归出口如何定义,这里只需要求符合条件的序列的数量，所有不需要返回真正的序列
```
    // 全排列
    public int countArrangement(int n) {
        boolean[] flag = new boolean[n+1];
        return countArrangement(n, 1, flag);
    }
    // 对于数字N,从beginIndex到n的都是需要填的空位置,还有多少个合法排列
    public int countArrangement(int n, int beginIndex, boolean[] flag){
        // beginIndex为n+1时,表明1~n位置的数都排列好了
        if(beginIndex==n+1){
            return 1;
        }
        int count = 0;
        // 遍历1~n数字,尝试放到第beginIndex位置上
        for(int i=1;i<=n;i++){
            if(!flag[i] && (i%beginIndex==0 || beginIndex%i==0)){
                flag[i] = true;
                count += countArrangement(n, beginIndex+1, flag);
                flag[i] = false;
            }
        }
        return count;
    }
```


#### leetcode-46.全排列  
思路: DFS + 回溯+状态数组,同leetcode-526

#### leetcode-697.数组的度
>思考:求最大出现频率的数,频率用{value:frequency}统计,这种最值问题比如最小数、最大数,都可以在遍历过程中得到.  

思路: 找到所有可能的最大频率的元素，计算这些元素的lastPos-firstPos+1的最小值
解法1:countMap统计每个元素出现的频率，firstMap来记录每个元素第一次出现的位置，degree变量表示当前频率最大,Length表示所求最小连续子数组长度，遍历数组，对于每个当前遍历的元素x,如果x的频率大于degree，则更新degree并赋值minLenghth为currentPosOfx-firstPosOfx+1，如果其频率等于degree，则minLenghth = math.min(minLenghth, currentPosOfx-firstPosOfx+1)
解法2:定义一个数据结构pair,扫描数组得到所有元素对应的map:{value:pair},最后得到最大degree对应的最小连续子数组长度
```
class pair{
  int first;
  int last;
  int degree;
}
```
[参考](https://leetcode.com/problems/degree-of-an-array/discuss/124317/JavaC%2B%2BPython-One-Pass-Solution)

#### leetcode-766.托普利茨矩阵
题目描述: 如果矩阵上每一条由左上到右下的对角线上的元素都相同，那么这个矩阵是托普利茨矩阵
思路:
(1)解法1:每次遍历一条对角线,监测该对角线上的元素是否满足,遍历第一排和第一列的每个元素，遍历到一个元素a，坐标为(x,y)时，就一直沿着其右下方对角线遍历，既x++,y++; 检测对角线上的元素值是否一样,需要检测是否越界
(2)解法2:没必要一次遍历一条对角线,只要遍历完对角线上所有元素即可,而且只有一个元素的对角线不用遍历,所以需要遍历的行范围是[0,matrix.length-1], 列范围[0,matrix[0].length-1],对于范围内的每个元素的坐标为(x,y)，检测
matrix[x][y]是否等于matrix[x+1][y+1]即可，比解法1简洁,不需要判断是否范围溢出

#### leetcode-565.数组嵌套  
题目描述: https://leetcode-cn.com/problems/array-nesting/
思路:可以证明任给一个index=x开始,index对应的值A[x]，设y=A[x],则下一个数为A[y]，设z=A[y],再下一个数为A[z]，最后必然得到A[x]  
则所有0到N-1的这N个index可以分为好几组，每一组都形成一个环，且每一组的环都和别的组的环不相交，题目要求的就是这些环中的最大环长度，所以我们遍历任意一个元素都只需要遍历一遍，因为这个元素只属于一个环，
则一个index被遍历后就标记这个index，比如可以设置A[index]为-1，当遍历到一个A[x]为-1时直接i跳过即可
```
    // 标记法,事件复杂度O(N)
    public int arrayNesting(int[] nums) {
        int maxCount = 0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]==-1){
                continue;
            }
            // 得到一个环的第一个数  
            int frequency = 1;
            int x = nums[i];
            nums[i] = -1;
            while(nums[x]!=-1){
                int temp = nums[x];
                nums[x] = -1;
                x = temp;
                frequency++;
            }
            maxCount = Math.max(maxCount, frequency);
        }
        return maxCount;
    }
```
#### leetcode-769.最多能完成排序的块
思路:要找到最多的块,所以每个块就要尽可能小,从左边开始找第一个符合条件的最小块,一个符合条件的块[0,1,2,k]必然满足块中的最大值等于该块最最右边元素的index
```
    public int maxChunksToSorted(int[] arr) {
        int count = 0;
        // 初始化为-1
        int curMax = -1;
        for(int i=0;i<arr.length;i++){
            curMax = Math.max(curMax, arr[i]);
            if(curMax==i){
                count++;
                curMax = -1;
            }
        }
        return count;
    }
```
#### leetcode-1.两数之和
题目描述: 给一个数组,和一个值target,判断数组中是否存在两个数使其和等于target  
思路:  
(1)双指针-顺序查找
(2)双指针-二分查找
扫描数组,对扫描的每个数作为left,对left右边的数组的部分进行二分查找
(3)map

#### leetcode-1-变种  
题目描述:给一个数组,求数组是否存在两个数的和等于target,返回这两个数的index,这样的两个数可能有很多对,返回所有对的不重复的两个数的index  
思路:关键是去重   
```
public List<List<Integer>> twoSumMultiple(int[] nums, target){
  Arrays.sort(nums);
  List<Integer> res = new ArrayList<>();
  int low = 0, high = nums.length - 1;
    
}
```
#### leetcode-15.三数之和  
>就是leetcode-1-变种加了一层循环

思路:排序+双指针,时间O(N*N)
```
    // 关键是如何去重:选取第一个数时要去重,选取第2,3个数时要去重
    // https://leetcode-cn.com/problems/3sum/solution/pai-xu-shuang-zhi-zhen-zhu-xing-jie-shi-python3-by/
    public List<List<Integer>> threeSum(int[] nums) {
        if(nums==null || nums.length<3){
            return new ArrayList<List<Integer>>();
        }
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        for(int i=0;i<nums.length-2;i++){
            // 第一个数去重
            if(i>0 && nums[i]==nums[i-1]){
                continue;
            }
            int low = i+1, high = nums.length-1;
            int target = -nums[i];
            while(low<high){
                int sum = nums[low] + nums[high];
                if(sum == target){
                    res.add(Arrays.asList(nums[i],nums[low], nums[high]));
                    // 第二三个数left去重
                    while(low<high && nums[low]==nums[low+1]){
                        low++;
                    }
                    // 第二三个数right去重
                    while(low<high && nums[high]==nums[high-1]){
                        high--;
                    }
                    low++;
                    high--;
                }else if(sum < target){
                    low++;
                }else{
                    high--;
                }
            }
        }
        return res;
    }
```
#### leetcode-16.最接近的三数之和
思路:因为只有唯一一对数满足条件,所以不考虑去重
[参考](https://leetcode-cn.com/problems/3sum-closest/solution/hua-jie-suan-fa-16-zui-jie-jin-de-san-shu-zhi-he-b/)
#### leetcode-18. 四数之和
思路:类似于leetcode-15,有多对数满足条件,需要考虑去重
[参考](https://leetcode-cn.com/problems/4sum/solution/si-shu-zhi-he-by-leetcode-solution/)
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