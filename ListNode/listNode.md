**83 [删除排序链表中的重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/)**

给定一个已排序的链表的头 `head` ， *删除所有重复的元素，*使每个元素只出现一次* 。返回 *已排序的链表* 。*

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode p = head;
        while(p!=null){
            while(p.next!=null&&p.val==p.next.val){
                p.next=p.next.next;
            }
            p=p.next;
        }
        return head;
    }
}
```

只需要判断下一个节点与该节点的值是否相同，如果相同则向后跳。注意如果反过来则会产生空指针异常

```java
while(p.next!=null&&p.val!=p.next.val){
	p=p.next;
}
p.next=p.next.next;
```

因为如果p是最后一个节点，则p.next==null，这个时候p.next.next获取不到。

**82 [删除排序链表中的重复元素 II](https://leetcode.cn/problems/remove-duplicates-from-sorted-list-ii/)**

给定一个已排序链表，删除所有的重复元素，返回链表。与上一题不同的是重复元素全部删除掉。

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null){
            return head;
        }
        ListNode dummy = new ListNode(-1,head);
        ListNode p = dummy;
        int n = 0;
        while(p.next!=null&&p.next.next!=null){
            if(p.next.val==p.next.next.val){
                n=p.next.val;
                while(p.next!=null&&p.next.val==n){
                    p.next=p.next.next;
                }
            }else{
                p=p.next;
            }
        }
        return dummy.next;
    }
}
```

第一个head节点很有可能被删除掉，所以用一个dummy节点来去取代。然后用一个p节点来去在链表上进行操作，去掉重复的元素。 **与上一题相同，p向后移动的条件仅出现在当两个相邻元素的值不相等时。如果相等就需要进行去重了**


**[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)**

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

完成链表的转向需要3个指针，一个指到pre节点，一个当前节点，一个post节点

当前节点的next指向pre

```java
public ListNode reverseList(ListNode head) {
    ListNode pre = null, p = head;
    while(p!=null){
      ListNode temp = p.next;
      p.next = pre;
      pre = p;
      p = temp;
}
return pre;
```

分享一个递归的方式：

```java
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        //直到走到最后一个节点
        ListNode newhead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newhead;
    }
```

**[92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)**

给你单链表的头指针 `head` 和两个整数 `left` 和 `right` ，其中 `left <= right` 。请你反转从位置 `left` 到位置 `right` 的链表节点，返回 **反转后的链表** 。

<img src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" alt="img" style="zoom:33%;" />

```
输入：head = [1,2,3,4,5], left = 2, right = 4
输出：[1,4,3,2,5]
```

```
输入：head = [5], left = 1, right = 1
输出：[5]
```

总体思想就是分为3段，前面不需要变动的为1段，中间反转的走上面的反转链表流程，后面不需要变动的为1段，之后拼接起来即可。  

```java
public ListNode reverseBetween(ListNode head, int left, int right) {
        //因为有可能整个反转，所以存在第一个节点丢失问题，因此我们引入newHead
        ListNode newHead = new ListNode(0,head);
        ListNode p = newHead;
        for(int i=0; i<left-1; i++){
            p=p.next;
        }
        ListNode pre = null;
        ListNode cur = p.next;
        //截取出来中间的反转部位来做反转
        for(int i = left; i<=right;i++){
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        p.next.next = cur;
        p.next=pre;
        return newHead.next;
    }
```

**[21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)**

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

<img src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" alt="img" style="zoom:33%;" />

```java
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0), p = dummy;
        while (l1 != null && l2 != null) {
            p = (p.next = (l1.val < l2.val) ? l1 : l2);
            if (p == l1) l1 = l1.next; else l2 = l2.next;
        }
        p.next = l1 != null ? l1 : l2;
        return dummy.next;
    }
```


