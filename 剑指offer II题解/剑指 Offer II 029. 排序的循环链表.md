#### [剑指 Offer II 029. 排序的循环链表](https://leetcode.cn/problems/4ueAj6/)

给定循环单调非递减列表中的一个点，写一个函数向这个列表中插入一个新元素 insertVal ，使这个列表仍然是循环升序的。

给定的可以是这个列表中任意一个顶点的指针，并不一定是这个列表中最小元素的指针。

如果有多个满足条件的插入位置，可以选择任意一个位置插入新的值，插入后整个列表仍然保持有序。

如果列表为空（给定的节点是 null），需要创建一个循环有序列表并返回这个节点。否则。请返回原先给定的节点。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2019/01/19/example_1_before_65p.jpg)

~~~
输入：head = [3,4,1], insertVal = 2
输出：[3,4,1,2]
解释：在上图中，有一个包含三个元素的循环有序列表，你获得值为 3 的节点的指针，我们需要向表中插入元素 2 。新插入的节点应该在 1 和 3 之间，插入之后，整个列表如上图所示，最后返回节点 3 。
~~~

![img](https://assets.leetcode.com/uploads/2019/01/19/example_1_after_65p.jpg)

**示例 2：**

~~~
输入：head = [], insertVal = 1
输出：[1]
解释：列表为空（给定的节点是 null），创建一个循环有序列表并返回这个节点。
~~~

**示例 3：**

~~~
输入：head = [1], insertVal = 0
输出：[1,0]
~~~

**提示：**

~~~
0 <= Number of Nodes <= 5 * 10^4
-10^6 <= Node.val <= 10^6
-10^6 <= insertVal <= 10^6
~~~



#### 题解

~~~java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _next) {
        val = _val;
        next = _next;
    }
};
*/

class Solution {
    public Node insert(Node head, int insertVal) {
        Node node=new Node(insertVal);
        node.next=node;
        if(head==null){
            return node;
        }
        int max=head.val;
        int min=head.val;
        Node ans=head;
        while(head.next!=ans){
            head=head.next;
            max=Math.max(max,head.val);
            min=Math.min(min,head.val);
        }

        if(max==min){
            node.next=ans.next;
            ans.next=node;
        }else{
            while(!(head.val==max&&head.next.val==min)){
                head=head.next;
            }
            while(!(insertVal<=min||insertVal>=max)&&!(insertVal<=head.next.val&&head.val<=insertVal)){
                head=head.next;
            }
            node.next=head.next;
            head.next=node;
        }
        return ans;
    }
}
~~~

时间复杂度：O(n)  

分析：先遍历了一次找最大值最小值，后面寻找插入位置时再遍历一次，因此是O(n)

空间复杂度：O(1)