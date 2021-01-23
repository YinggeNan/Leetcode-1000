#### 原地反转链表in-place reversal of a linkedlist 
1-Reverse a LinkedList (easy)
2-Reverse a Sub-list (medium)
3-Reverse every K-element Sub-list (medium)

#### Intersection of Two Linked Lists (Easy)
题目描述: 找到两个单链表的交点  
思路:   
(1)空间O(N)-set，两个链表的第一个重复的节点就是交点  
(2)双指针P1,p2；p1指向head1，p2指向head2，同时开始遍历当p1为null时将p1指向head2，当p2为null时将p2指向head1；如果两个链表没有交点，那么p1、p2最终会同时指向null，可以画图模拟  

#### Reverse Linked List (Easy)
题目描述: 翻转一个单链表  
思路:   
(1)栈空间O(N)，从head开始把链表所有节点入栈然后逐一弹出尾插法重建链表  
(2)递归：定义一个函数返回翻转后的所有链表，比如f(node)返回将以node为头节点的链表翻转的头节点，注意到f(node.next)翻转后的尾节点就是node.next;   
(3)迭代：扫描链表采用dummy头节点+头插法重建链表  

#### Merge Two Sorted Lists (Easy)
题目描述: 给两个从头节点递增排序的单链表，将其归并为一个递增排序的单链表  
思路:   
(1)迭代+双指针+选取较小节点尾插法重建单链表  
(2)递归:定义mergeTwoSortedList(l1, l2)返回以l1、l2分别为头节点的递增排序单链表归并后的单链表，重点是当l1<=l2时，l1.next = mergeTwoSortedList(l1.next, l2)，返回l1.  

#### Remove Duplicates from Sorted List (Easy)
题目描述: 给一个从头节点开始递增排序的链表，去掉所有重复的数字  
思路:  
(1)迭代+dummy+尾插法重建链表  
(2)递归：关键是是如何去重,有两种写法
```
    // 第一种
    // deleteDuplicates返回删除了所有重复值的链表的头节点
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode nextNode = head.next;
        // 删除所有重复值，保证nextNode和head的val一定不一样
        while(nextNode!=null && head.val==nextNode.val){
            nextNode = nextNode.next;
        }
        head.next = deleteDuplicates(nextNode);
        return head;
    }
```
```
    // 第二种
    // deleteDuplicates返回删除了所有重复值的链表的头节点
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        head.next = deleteDuplicates(head.next);
        // head.next=deleteDuplicates(head.next)，函数定义保证了以head.next开头的链表中没有重复值了
        // 所以只要判断head和head.next是否相同即可
        return head.val==head.next.val?head.next:head;
    }
```

#### Remove Nth Node From End of List (Medium)
题目描述: 删除链表的倒数第 n 个节点
思路: 双指针，设置p1,p2指针，让p1比p2先跑n+1步，然后p1,p2一起以1为步长一起跑，当p1为null时，p2就是倒数第n个节点的前驱了，注意corner case，当n为链表长度时需要删除头节点，
两种方式处理删除头节点(1)先让p1跑n步，如果p1这时为null直接返回head.next（2）设置一个dummy节点，令dummy.next = head,让p1和p2都从dummy节点开始，则头节点也有前驱节点了
#### 交换链表中的相邻结点
题目描述:  交换链表中的相邻结点  
思路:  
(1)递归
```
    // 同时取链表的相邻的2个节点交换位置
    // swapPairs返回以head为头节点的交换了相邻两个节点位置的新链表的头节点
    public ListNode swapPairs(ListNode head) {
        // 一个节点不需要交换
        if(head==null|| head.next==null){
            return head;
        }
        // 交换head和head.next
        ListNode temp = head.next.next;
        ListNode root = head.next;
        root.next = head;
        // 处理子链表
        head.next = swapPairs(temp);
        return root;
    }
```
(2)迭代：p每次选取一个pair，交换pair中的两个节点，然后将pair放回原位置，然后p = p.next.next.next，直到选不出一个pair  
#### Add Two Numbers II (Medium)
题目描述: 给两个链表l1、l2，l1和l2各代表一个数字，每个节点代表数字的一位（十进制），头节点是最高位，从头节点到尾节点依次降低到个位，求两个链表的和，和也用一个头节点表示最高位而尾节点表示最低位的链表表示  
***不能将l1、l2逆序
思路: 正常遍历链表的顺序是从头节点到尾节点，但是这样得到是数字的最高位到最低位，无法用来求和，所以借助两个栈得到两个链表的逆序表示然后求和

#### Palindrome Linked List (Easy)
题目描述: 判断一个链表是不是回文链表，要求空间复杂度O(1)  
思路: 通过得到链表的从左向右和从右向左的遍历序列s1、s2然后判断是否相等即可  
(1)借助栈得到链表的逆序表示，但是空间为O(N)不满足  
(2)首先用快慢指针找到链表的后半段的第一个节点rightHalfFirstNode，然后将后半段逆序，再对比前半段和逆序后的后半段是否值都相等即可  
```
    public boolean isPalindrome(ListNode head) {
        if(head==null || head.next == null){
            return true;
        }
        ListNode head1 = reverse(halfHeadOfRight(head));
        while(head1!=null){
            if(head1.val!=head.val){
                return false;
            }
            head1 = head1.next;
            head = head.next;
        }
        return true;
    }
    // 链表head有奇数个节点时slow为中间节点，偶数个节点时slow为前半段最后一个节点
    // 则无论链表长度为奇数还是偶数，后半段开始的节点都是low.next
    public ListNode halfHeadOfRight(ListNode head){
        if(head==null || head.next == null){
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast!=null && fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow.next;
    }
    public ListNode reverse(ListNode head){
        if(head == null || head.next==null){
            return head;
        }
        ListNode tail = head.next;
        ListNode root = reverse(head.next);
        tail.next = head;
        // 截断破除循环
        head.next = null;
        return root;
    }
```

#### Split Linked List in Parts(Medium)
题目描述: 分隔链表，给一个链表，要求将其分成k段，且任何两段之间的节点数量差值不能超过1，所以有可能有些段节点数量为0，而且前面的段的节点数量>=后面的段
思路: 得到链表长度L，每个段都有的节点最少值average = L/K, 还剩下可以给L%K个段(从第一个段开始向后逐次分配)每个段多分配一个

#### Odd Even Linked List (Medium)
题目描述: 链表元素按奇偶index聚集
思路: 双指针odd、even按照奇偶count重建链表然后将偶段连接在奇段后面即可