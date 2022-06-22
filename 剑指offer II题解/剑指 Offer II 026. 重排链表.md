#### [剑指 Offer II 026. 重排链表](https://leetcode.cn/problems/LGjMqU/)

给定一个单链表 L 的头节点 head ，单链表 L 表示为：

 L0 → L1 → … → Ln-1 → Ln 
请将其重新排列后变为：

L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …

不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

**示例 1:**

![img](https://pic.leetcode-cn.com/1626420311-PkUiGI-image.png)

```
输入: head = [1,2,3,4]
输出: [1,4,2,3]
```

**示例 2:**

![img](https://pic.leetcode-cn.com/1626420320-YUiulT-image.png)

```
输入: head = [1,2,3,4,5]
输出: [1,5,2,4,3]
```

<img src="C:\Users\86152\AppData\Roaming\Typora\typora-user-images\image-20220621121206235.png" alt="image-20220621121206235" style="zoom: 80%;" />



#### 题解

思路：利用虚拟头节点+快慢指针，找到链表中间节点，反转后半部分链表，再进行交替拼接即可。

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
    public void reorderList(ListNode head) {
        // 长度为1的链表无需变化
        if(head.next==null){
            return;
        }
        // 虚拟头结点
        ListNode virHead=new ListNode(0);
        virHead.next=head;
        ListNode p1=virHead;
        ListNode p2=head;
        // 快慢指针获取链表中点位置
        while(p2!=null&&p2.next!=null){
            p1=p1.next;
            p2=p2.next.next;
        }

        // 截取后半段链表，进行反转
        ListNode p=reverseNode(p1.next);
        p1.next=null;
        p1=head; // 第一个指针指向第一个链表头部
        p2=p;   // 第二个指针指向反转后的链表头部

        // 拼接两个链表
        while(p1!=null&&p2!=null){
            ListNode t1=p1.next;
            ListNode t2=p2.next;
            p1.next=p2;
            if(t1==null){
                break;
            }
            p2.next=t1;
            p1=t1;
            p2=t2;
        }
    }
    /**
        反转链表
     */
    public ListNode reverseNode(ListNode head){
        if(head==null||head.next==null){
            return head;
        }
        ListNode p1=head;
        ListNode p2=head.next;
        ListNode curHead=head;  
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

