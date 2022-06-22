#### [剑指 Offer II 021. 删除链表的倒数第 n 个结点](https://leetcode.cn/problems/SLwz0R/)

给定一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```

**提示：**

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`



#### 题解

创建虚拟头节点，移动两个指针完成替换

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // 避免head为空的情况
        if(head==null){
            return head;
        }
        // 虚拟头节点
        ListNode virHead=new ListNode(0);
        ListNode p1=virHead;
        ListNode p2=p1;
        virHead.next=head;
        // 先将p1和p2两个指针相差长度为n
        while(n!=0&&head!=null){
            p2=p2.next;
            n--;
        }
        // 同时向右移动至链表末尾，使p2指向最后一个元素
        while(p2.next!=null){
            p1=p1.next;
            p2=p2.next;
        }
        // 清除目标节点(p1.next)
        ListNode temp=p1.next;
        p1.next=temp.next;
        temp.next=null;
        // 返回真正的头节点
        return virHead.next;
    }
}
~~~

