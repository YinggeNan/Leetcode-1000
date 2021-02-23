#### leet


#### Leetcode-232.用栈实现队列
思路: 设置两个栈A、B，入队push进入栈A，出队从栈B pop出来，栈B为空时将栈A所有元素出栈再依次入栈B  

#### leetcode-155.最小栈
思路: 设置两个栈dataStack、minStack, 往dataStack push进入一个元素x后往minStack push一个当前stack中的最小值xMin,  
dataStack的每一层的数字x都对应minStack同层的一个xMin, xMin代表当x成为栈顶元素时栈中的最小值,   
如何计算xMin呢? 设置一个全局变量min，当push一个值x时，如果$x<min$，那么更新min=x，将x push进入dataStack后，将min push进入minStack
>最大栈
#### leetcode-20.有效的括号
题目描述: 对输入只有三种括号的字符串检测是否括号匹配，()[]{}  
思路: 栈，扫描输入字符,a.当栈为空时字符入栈,b.当栈不为空时查看栈顶字符和扫描字符是否匹配,如果匹配则栈poll，不匹配则入栈,扫描输入字符串完毕后，如果栈为空则括号匹配
#### leetcode-1047.删除字符串中的所有相邻重复项

#### leetcode-739.每日温度  
题目描述: 数组中元素与下一个比它大的元素之间的距离  
思路: 遍历数组时用栈把数组中的数存起来，如果当前遍历的数比栈顶元素来的大，说明栈顶元素的下一个比它大的数就是当前元素
#### leetcode-503.下一个更大元素II
题目描述: 循环数组中比当前元素大的下一个元素  
思路: 和Daily Temperatures类似，但对于位置为index的数，可以查找index左边是否存在比index位置大的元素，则设置遍历范围为两倍长数组度, 对遍历变量i取模得到在数组中的位置，且只将0~n-1范围的元素加入栈

