#### [剑指 Offer II 025. 链表中的两数相加](https://leetcode.cn/problems/lMSNwu/)

给定两个 非空链表 l1和 l2 来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

可以假设除了数字 0 之外，这两个数字都不会以零开头。

**示例1：**

![img](https://pic.leetcode-cn.com/1626420025-fZfzMX-image.png)

```
输入：l1 = [7,2,4,3], l2 = [5,6,4]
输出：[7,8,0,7]
```

**示例2：**

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[8,0,7]
```

**示例3：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

<img src="C:\Users\86152\AppData\Roaming\Typora\typora-user-images\image-20220621151910161.png" alt="image-20220621151910161" style="zoom:67%;" />

**进阶：**如果输入链表不能修改该如何处理？换句话说，不能对列表中的节点进行翻转。



#### 题解

思路：先反转两个链表，再逐个节点遍历的同时，相加每一位的值，采用头插法创建新的链表

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head=new ListNode(0);
        ListNode head1=reverse(l1);
        ListNode head2=reverse(l2);
        int carry=0;//进位
        int sum=0;//和
        ListNode p1=head1;
        ListNode p2=head2;
        ListNode p=head;
        while(p1!=null||p2!=null){
            int n1=p1==null?0:p1.val;
            int n2=p2==null?0:p2.val;
            sum=n1+n2+carry;
            carry=sum/10;
            ListNode node=new ListNode(sum%10);
            node.next=p.next;
            p.next=node;
            if(p1!=null){
                p1=p1.next;
            }
            if(p2!=null){
                p2=p2.next;
            }
        }
        if(carry!=0){
            ListNode node=new ListNode(carry);
            node.next=p.next;
            p.next=node;
        }
        return head.next;
    }

    public ListNode reverse(ListNode head){
        ListNode pHead=head;
        ListNode p1=head;
        ListNode p2=p1.next;
        while(p2!=null){
            p1.next=p2.next;
            p2.next=pHead;
            pHead=p2;
            p2=p1.next;
        }
        return pHead;
    }
}
~~~

