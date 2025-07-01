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
