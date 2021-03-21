### <a id="_link_click_group">LeetCode-栈(Stack)-easy-题单</a>
##### [LeetCode-.有效的括号](#_id)
##### [LeetCode-155.最小栈](#_id155)
##### [LeetCode-225.用队列实现栈](#_id225)
##### [LeetCode-232.用栈实现队列](#_id232)
##### [LeetCode-496.下一个更大元素I](#_id496)
##### [LeetCode-682.棒球比赛](#_id682)
##### [LeetCode-844.比较含退格的字符串](#_id844)
##### [LeetCode-1021.删除最外层的括号](#_id1021)
##### [LeetCode-1047.删除字符串中的所有相邻重复项](#_id1047)
##### [LeetCode-1441.用栈操作构建数组](#_id1441)
##### [LeetCode-1544.整理字符串](#_id1544)
##### [LeetCode-1598.文件夹操作日志搜集器](#_id1598)


### 括号匹配
leetcode-394.字符串解码  
思路:此题用DFS不好求,用栈好解答  
```
    // 括号匹配问题,使用栈解决
    // 为]时出栈, 字母连续出栈, 数字连续出栈
    // 不为]时入栈
    public String decodeString(String s) {
        // 栈中最后保存重复后的所有字母
        List<Character> stack = new LinkedList<>();
        for(char c: s.toCharArray()){
            if(c!=']'){
                stack.add(c);
            }else{
                // 将所有字母出栈,逆序(头插法)
                List<Character> res = new LinkedList<>();
                while(stack.get(stack.size()-1)!='['){
                    res.add(0, stack.remove(stack.size()-1));
                }
                // 将'['出栈
                stack.remove(stack.size()-1);
                 // 将所有数字出栈
                List<Character> numberStr = new LinkedList<>();
                while(stack.size()>0 && stack.get(stack.size()-1)>=48 && stack.get(stack.size()-1)<=57){
                    numberStr.add(0, stack.remove(stack.size()-1));
                }
                int number = parseNumber(numberStr);
                int len = res.size();
                // 重复方括号内字母number次并入栈
                for(int i=0;i<number;i++){
                    for(int j=0;j<len;j++){
                        stack.add(res.get(j));
                    }
                }
            }
        }
        StringBuilder resStr = new StringBuilder();
        for(int i=0;i<stack.size();i++){
            resStr.append(stack.get(i));
        }
        return resStr.toString();
    }
    public int parseNumber(List<Character> numberStr){
        int sum = 0;
        for(char c: numberStr){
            sum = sum*10 + c - '0';
        }
        return sum;
    }
```
### LeetCode-栈(Stack)-easy-题解
##### <a id="_id">[LeetCode-.有效的括号](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id155">[LeetCode-155.最小栈](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id225">[LeetCode-225.用队列实现栈](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id232">[LeetCode-232.用栈实现队列](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id496">[LeetCode-496.下一个更大元素I](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id682">[LeetCode-682.棒球比赛](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id844">[LeetCode-844.比较含退格的字符串](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id1021">[LeetCode-1021.删除最外层的括号](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id1047">[LeetCode-1047.删除字符串中的所有相邻重复项](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id1441">[LeetCode-1441.用栈操作构建数组](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id1544">[LeetCode-1544.整理字符串](#_link_click_group)</a>
题目描述:
思路:
```

```
##### <a id="_id1598">[LeetCode-1598.文件夹操作日志搜集器](#_link_click_group)</a>
题目描述:
思路:
```

```
