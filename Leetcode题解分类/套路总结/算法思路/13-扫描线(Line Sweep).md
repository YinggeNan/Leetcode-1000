### LintCode-391.[Number of Airplanes in the Sky](https://www.lintcode.com/problem/number-of-airplanes-in-the-sky/description)
> 最大重叠区间数
#### 题目描述
给出飞机的起飞和降落时间的列表，用序列 interval 表示. 请计算出天上同时最多有多少架飞机？  
例子：
输入: [(1, 10), (2, 3), (5, 8), (4, 7)]  
输出: 3  
解释:   
第一架飞机在1时刻起飞, 10时刻降落.  
第二架飞机在2时刻起飞, 3时刻降落. 
...
在5时刻到6时刻之间, 天空中有三架飞机.  
#### 思路1：扫描线算法  
按照扫描线算法标准思路，把所有起飞、降落时刻包装成event，在天上的飞机数为count，对所有event按照时间排序，起飞event则count+1，降落event则count-1  
排序时对同一时刻的起飞和降落event，保证降落event在前起飞event前面，对所有event排序后扫描event数组，对每个event后统计全局最大count数  
时间复杂度O(NlogN),空间复杂度O(N)
> 扫描线算法可以应对多个区间重叠求最大重叠区间数的问题，而且是在区间两端处统计重叠次数
#### 思路2：前缀和  
首先得到最大时刻（肯定是降落）M，设置一个长M的数组time，然后扫描intervals数组，每个起飞时刻i，则time[i]++，对每个降落时刻则time[i]--，再计算time的前缀和数组prefix，最后求prefix中的最大值即可，  
时间O(M)，空间O(M)，对于特殊情况很容易内存溢出
而且起飞降落时刻相同时，还需要特别处理，不能直接time[i]++或time[i]--，要类似于哈希表使用拉链表存储（降落在前、起飞在后）
treemap只适合求overlap个数的问题
### 思路3：TreeMap
其实还是扫描线算法，不过就是用TreeMap来排序罢了
TreeMap参考：https://www.liaoxuefeng.com/wiki/1252599548343744/1265117109276544
### lintCode-919.[meeting-rooms-ii](https://www.lintcode.com/problem/meeting-rooms-ii/description)
> 最大重叠区间数
#### 题目描述
给定一系列的会议时间间隔intervals，包括起始和结束时间[[s1,e1],[s2,e2],...] (si < ei)，找到所需的最小的会议室数量。
例子：
输入: intervals = [(0,30),(5,10),(15,20)]
输出: 2
解释:
需要两个会议室
会议室1:(0,30)
会议室2:(5,10),(15,20)
#### 思路1: 扫描线算法
就是求任一时刻同时在开会的最多会议数量就是需要的最少会议室数量，所有把会议开始时刻和会议结束时刻包装成event，count表示某一时刻同时在开的会议数量，
扫描到一个开始event则count+，扫描到一个结束event，则count-1,
#### 思路2：前缀和
类似于LintCode391
### lintcode-821.[Time Intersection](https://www.lintcode.com/problem/time-intersection/note/209862)
> 所有重叠区间数量
#### 题目描述
目前有两个用户的有序在线时间序列，每一个区间记录了该用户的登录时间点x和离线时间点y，请找出这两个用户同时在线的时间段，输出的时间段请从小到大排序。你需要返回一个intervals的列表
例子：
输入：seqA = [(1,2),(5,100)], seqB = [(1,6)]
输出：[(1,2),(5,6)]
解释：在 (1,2), (5,6) 这两个时间段内，两个用户同时在线。
#### 思路1-扫描线算法 
将所有登录、登出时刻包装为event，然后对event数组根据时刻排序，count为同时在线的人数，count从1->2时的时刻start是两个人都在线的时刻，count从2->1时是有一个人下线的时刻end(本次都在线的结束时刻)，
所以相邻的一组(start,end)就是同时在线的一个区间，将区间加入结果list接口，得到的在线区间必然是按照时刻升序排列的
#### 思路2：双指针求overlap
seqA和seqB的数据已经是升序且同一个seq的任意两个区间不会相交，指针p1从seqA出发，p2从seqB出发，然后可以和merge array一样，如果Max(startA, startB) < Min(endA, endB)则加入相交的interval 然后看A, B end 谁大，谁留下，另外一个踢走
> 双指针求重叠区间，必须seq1和seq2本身的区间不能重叠才行
### leetcode-1229.Meeting Scheduler
> 第一个符合长度要求的重叠区间
#### 题目描述：
Given the availability time slots arrays slots1 and slots2 of two people and a meeting duration duration, return the earliest time slot that works for both of them and is of duration duration.  
If there is no common time slot that satisfies the requirements, return an empty array.  
The format of a time slot is an array of two elements [start, end] representing an inclusive time range from start to end.    
It is guaranteed that no two availability slots of the same person intersect with each other. That is, for any two time slots [start1, end1] and [start2, end2] of the same person, either start1 > end2 or start2 > end1.  
例子： 
Input: slots1 = [[10,50],[60,120],[140,210]], slots2 = [[0,15],[60,70]], duration = 8
Output: [60,68]  
#### 思路-双指针打擂台
题目要求的是时间最早的重叠长度符合要求的重叠区间，所以对slots1和slots2分别按照每个区间的startTime排序照双指针打擂台，找到第一个符合长度要求的重叠区间就返回，没找到时，抛弃endTime较小的区间
题目保证了slots和slots2都满足属于同一个slot的任意两个区间不会相交，所以可以用双指针
```
class Solution {
    public List<Integer> minAvailableDuration(int[][] slots1, int[][] slots2, int duration) {
        List<Integer> list = new ArrayList<Integer>();
        Arrays.sort(slots1, (a, b) -> (a[0] - b[0]));
        Arrays.sort(slots2, (a, b) -> (a[0] - b[0]));
        
        int a = 0; int b = 0;
        while(a < slots1.length && b < slots2.length) {
            // start 取最大，end 取最小；
            int start = Math.max(slots1[a][0], slots2[b][0]);
            int end = Math.min(slots1[a][1], slots2[b][1]);
            if(start < end && end - start >= duration) {
                list.add(start);
                list.add(start + duration);
                return list;
            } else {
                if(slots1[a][1] < slots2[b][1]) {
                    a++;
                } else {
                    b++;
                }
            }
        }
        return list;
    }
}
```
### Leetcode-218.[The Skyline Problem-Hard](https://leetcode-cn.com/problemset/all/?search=Skyline%20problem)
思路：
题目的真正意思是输出所有的转折点（是所有建筑左右端点集合的子集，包括了一部分建筑的左端点+交点，不包括任何右端点），转折需要通过扫描经过的建筑端点高度来判断，记录上一次转折点的高度，如果本次扫描到的  
端点的高度和上一次转折点的高度不同，则本次端点为转折点
将所有的建筑的每个端点（左右端点）包装成一个pair，然后按照x轴排序    
TreeMap存放{height:count}，为什么要用TreeMap不用TreeSet，因为可能连续存在多个高度相同的建筑。  
扫描中状态：如果一个建筑的左端点被扫描线经过，但其右端点还没有经过，就称其为扫描中状态，以其高度为key加入处于扫描中状态的TreeMap中，当扫到一个建筑的右端点时移除key=其高度的元素，表示将该建筑移除扫描中状态
存放扫描中状态的建筑的高度  
转折点：上一次转折点的高度maxHeight，初始为0，当扫描到一个端点时，如果扫描中状态（如果当前扫描的端点为右端点，将会从扫描中状态移除）的所有元素的最大高度不等于上一次转折点高度时，称遇到一个状态状态，就会有一个新的转折点，转折点的x坐标是当前被扫描的端点的x坐标，转折点的y坐标是扫描中状态TreeMap中的最大高度端点的y坐标
```
    // 扫描线：所有端点<x,y>组成的序列按照x排序
    // 扫描到一个建筑的左端点将其加入TreeMap，扫描到右端点将其移除TreeMap，TreeMap保存{height:count}
    // 为什么要用TreeMap不用TreeSet，因为可能存在连续相同高度且重叠的建筑
    // 使用TreeMap可以动态得到排序序列，而且是{key:value}结构
    // 此题其实只需要动态得到扫描中状态的最大高度，所以用TreeMap或PriorityQueue都可以
    // 但是删除操作而言PriorityQueue时间复杂度O(logN),而TreeMap为O(1)
    // 题目要得到的是转折点（一部分建筑的左端点+交点）
    // 转折状态：扫描到一个节点时，如果如果扫描中状态的所有节点的最大高度不等于上一个转折点的高度则说明遇到了一个新的转折点
    // 新转折点的x为当前被扫描端点的x，y为扫描中状态的最大高度
    public List<List<Integer>> getSkyline(int[][] buildings) {
        if(buildings==null || buildings.length==0){
            return new ArrayList<>();
        }
        List<Pair> endPoints = new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        for(int[] building:buildings){
            // 左坐标height用负值标记
            endPoints.add(new Pair(building[0], -building[2]));
            endPoints.add(new Pair(building[1], building[2]));
        }
        // 所有端点按照x轴顺序排序
        Collections.sort(endPoints, (a,b)->(a.x!=b.x?a.x-b.x:a.height-b.height));
        // {height:count}，倒序排序，最大值在最前面
        TreeMap<Integer,Integer> beScanning = new TreeMap<>((a, b) -> (b - a));
        // 初始化put，扫描线没有经过任何一个建筑时
        beScanning.put(0,1);
        int lastTurningPointHeight = 0;
        // 扫描所有端点
        for(Pair pair:endPoints){
            int height = pair.height;
            if(height<0){
                beScanning.put(-height, beScanning.getOrDefault(-height, 0)+1);
            }else{
                beScanning.put(height, beScanning.get(height)-1);
                if(beScanning.get(height)==0){
                    beScanning.remove(height);
                }
            }
            int maxHeight = beScanning.keySet().iterator().next();
            if(maxHeight!=lastTurningPointHeight){
                int x = pair.x;
                lastTurningPointHeight = maxHeight;
                res.add(Arrays.asList(x, lastTurningPointHeight));
            }
        }
        return res;
    }
    class Pair{
        int x;
        int height;
        Pair(int x, int height){ 
            this.x = x;
            this.height = height;
        }
    }
```
### lintcode-850.[Employee Free Time](https://www.lintcode.com/problem/employee-free-time/description)
#### 描述  
We are given a list schedule of employees, which represents the working time for each employee.  
Each employee has a list of non-overlapping Intervals, and these intervals are in sorted order.  
Return the list of finite intervals representing common, positive-length free time for all employees, also in sorted order.  
The Intervals is an 1d-array. Each two numbers shows an interval. For example, [1,2,8,10] represents that the employee works in [1,2] and [8,10].  
Also, we wouldn't include intervals like [5, 5] in our answer, as they have zero length.  
思路：对所有员工的登录登出信息包装成Moment，val为时刻，flag为-1表示登出，flag为1表示登入，count表示在线人数，对所有moment对象按照时刻升序排序
统计每个时刻的count，count从0-1时表示都不在线的区间，记录所有count从0->1的区间即可
``` 
    /**
     * @param schedule: a list schedule of employees
     * @return: Return a list of finite intervals 
     */
    public List<Interval> employeeFreeTime(int[][] schedule) {
        if(schedule==null || schedule.length==0){
            return new ArrayList<>();
        }
        List<Moment> moments = new ArrayList<>();
        for(int[] sc:schedule){
            for(int i=0;i<sc.length;i++){
                if(i%2==1){
                    // 登录
                    moments.add(new Moment(sc[i], -1));
                }else{
                    // 登出
                    moments.add(new Moment(sc[i], 1));
                }
            }
 
        }
        List<Interval> res = new ArrayList<>();
        int count=0;
        Collections.sort(moments, (a,b)->(a.val!=b.val?a.val-b.val:a.flag-b.flag));
        int sum = 0;
        int pre = Integer.MIN_VALUE;
        for(Moment moment:moments){
            int oldSum = sum;
            if(moment.flag<0){
                sum--;
            }else{
                sum++;
            }
            if(sum==0){
                pre = moment.val;
            }
            if(oldSum==0 && sum==1 && pre!=Integer.MIN_VALUE && moment.val>pre){
                res.add(new Interval(pre, moment.val));
            }
        }
        return res;
    }
    class Moment{
        int val = 0;
        int flag = 0;
        public Moment(int val, int flag){
            this.val = val;
            this.flag =flag;
        }
    }
```
### leetcode-554.[Brick Wall](https://leetcode-cn.com/problems/brick-wall/)
### leetcode-729.[My Calendar I](https://leetcode-cn.com/problems/my-calendar-i/)
### leetcode-731.[My Calendar II](https://leetcode-cn.com/problems/my-calendar-ii/)
### leetcode-732.[My Calendar III](https://leetcode-cn.com/problems/my-calendar-iii/)
### leetcode-391.[Perfect Rectangle](https://leetcode.com/problems/perfect-rectangle/)
### leetcode-850.[Rectangle Area II](https://leetcode.com/problems/rectangle-area-ii/)

### leetcode-1288.[Remove Covered Intervals](https://leetcode.com/problems/remove-covered-intervals/)
#### 思路
<strong>思路1-扫描线<strong/>  
如果一个区间被其他区间完全包裹，就称为一个被包裹区间，求有多少个被包裹区间   
<strong>1-1 对单个端点排序<strong/>  
可以将所有区间打散，变成左右端点，对于任意一个区间Range，如果扫描到其左端点时，你发现了其左端点左边还有其他区间的左端点，扫描到其右区间时你发现你右边还有其他区间的右端点.  
所以对于一个端点你需要标记是否为左/右端点，用count计数，扫描到左端点+1，扫描到右端点-1，  
但是对于range1[1,2]和range2[1,3]这种情况你必须把range1的左端点排到range2的左端点后面，所以对于相同值的左端点排序时，右边值大拍在前面  
但是对于range1[1,3]和range2[2,3]这种情况你必须把range1的右端点排到range2的左端点后面，所以对于相同值的右端点排序时，左边值大拍在后面  
说明对单个端点的排序是不科学的  
<strong>1-2 [直接对区间排序](https://leetcode-cn.com/problems/remove-covered-intervals/solution/sao-miao-xian-fa-by-liweiwei1419/) <strong/>  
对区间根据左端点升序排序，左端点值相同的右端点值大的放在前面  
<strong>思路2-[贪心](https://leetcode-cn.com/problems/remove-covered-intervals/solution/shan-chu-bei-fu-gai-qu-jian-by-leetcode-2/) <strong/>   
其实思路和扫描线一样。。
## [扫描线Sweep Line算法总结](https://blog.csdn.net/u013325815/article/details/103957911?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_title-6&spm=1001.2101.3001.4242)