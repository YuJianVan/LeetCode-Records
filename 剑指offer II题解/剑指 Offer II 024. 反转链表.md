#### [剑指 Offer II 024. 反转链表](https://leetcode.cn/problems/UHnkqh/)

给定单链表的头节点 `head` ，请反转链表，并返回反转后的链表的头节点。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

~~~
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
~~~

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```

**示例 3：**

~~~
输入：head = []
输出：[]
~~~

<img src="C:\Users\86152\AppData\Roaming\Typora\typora-user-images\image-20220620232908151.png" alt="image-20220620232908151" style="zoom: 67%;" />

#### 题解

思路：使用3个指针，利用头插法实现链表原地反转

~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head==null||head.next==null){
            return head;
        }
        ListNode p1=head;
        ListNode p2=head.next;
        ListNode curHead=p1;
        while(p2!=null){
            p1.next=p2.next;
            p2.next=curHead;
            curHead=p2;
            p2=p1.next;
        }
        return curHead;

    }
}
~~~

时间复杂度：O(n)   n=节点个数

空间复杂度：O(1)