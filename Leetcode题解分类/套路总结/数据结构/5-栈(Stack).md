#### Implement Queue using Stacks
题目描述: 用栈实现队列  

思路: 栈是LIFO，队列是FIFO，利用两个栈就可以实现FIFO；设置两个栈A、B，入队时push进入栈A，出队时，从栈B pop出来，栈B为空时将栈A所有元素出栈再依次入栈B  
#### Implement Stack using Queues (Easy)
题目描述: 用队列实现栈  
思路: 队列q进入一个元素x时，将队列q中所有除x以外的所有元素出队再入队

#### Min Stack (Easy)
题目描述: 最小(大)值栈

思路: 设置两个栈dataStack、minStack, 往dataStack push进入一个元素x后往minStack push一个当前stack中的最小值xMin  
&nbsp;所以dataStack的每一层的数字x都对应minStack同层的一个xMin, xMin代表当x成为栈顶元素时栈中的最小值  
&nbsp;如何计算xMin呢? 设置一个全局变量min，当push一个值x时，如果x<min，那么更新min=x，将x push进入dataStack后，将min push进入minStack
## Min Queue-编程之美3.7
题目描述: 最小(大)值队列，要求"O(1)时间获得当前队列中的最小(大)值

思路：
&nbsp;解法(1)：堆,将所有元素放进最小/大堆中，入队、出队时间复杂度为O(logN)  
&nbsp;解法(2)：用两个栈s1、s2实现队列，那么队列的最小值就是min(s1.min(), s2.min())，入队、出队时间复杂度为O(1)  
上述两种方法都是通过空间换时间达到了获取当前队列最小值时间复杂度为O(1)

#### Valid Parentheses (Easy)
题目描述: 对输入只有三种括号的字符串检测是否括号匹配，()[]{}  

思路: 栈，扫描输入字符,a.当栈为空时字符入栈,b.当栈不为空时查看栈顶字符和扫描字符是否匹配,如果匹配则栈poll，不匹配则入栈,扫描输入字符串完毕后，如果栈为空则括号匹配

#### Daily Temperatures (Medium)
题目描述: 数组中元素与下一个比它大的元素之间的距离

思路: 遍历数组时用栈把数组中的数存起来，如果当前遍历的数比栈顶元素来的大，说明栈顶元素的下一个比它大的数就是当前元素
#### Next Greater Element II (Medium)
题目描述: 循环数组中比当前元素大的下一个元素

思路: 和Daily Temperatures类似，但对于位置为index的数，可以查找index左边是否存在比index位置大的元素，则设置遍历范围为两倍长数组度, 对遍历变量i取模得到在数组中的位置，且只将0~n-1范围的元素加入栈
