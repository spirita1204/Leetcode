# 86. Partition List

Methods: Pointer
Difficulty: Medium

Medium

Topics

Companies

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/04/partition.jpg](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]

```

**Example 2:**

```
Input: head = [2,1], x = 2
Output: [1,2]

```

**Constraints:**

- The number of nodes in the list is in the range `[0, 200]`.
- `100 <= Node.val <= 100`
- `200 <= x <= 200`

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode partition(ListNode head, int x) {
        if(head == null) return head;
        // 首先找到第一个大于或等于给定值的节点，
        // 用题目中给的例子来说就是先找到4，
        // 然后再找小于3的值，每找到一个就将其取出置于4之前即可
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy;
        while (pre.next != null && pre.next.val < x) pre = pre.next;// 找到大於x前一位
        ListNode cur = pre;
        while (cur.next != null) {// 第一位大於小於皆沒差
            if (cur.next.val < x) {// cur = 4 cur.next = 2
                ListNode tmp = cur.next;// tmp = 2 需移動
                cur.next = tmp.next;// 4 -> 1
                tmp.next = pre.next;// 2 -> 4
                pre.next = tmp;// 1 -> 2
                pre = pre.next;// 指標移動到2
            } else {
                cur = cur.next;
            }
        }
        return dummy.next;
    }
}
```

```java
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
    // 兩種思路 1. 遇到移動指標 2.直接拆成兩個ListNode在串起來
    public ListNode partition(ListNode head, int x) {
        ListNode p1 = new ListNode(-1);
        ListNode p2 = new ListNode(-1);
        ListNode a = p1, b = p2;
        while(head != null) {
            if(head.val < x) {
                p1.next = new ListNode(head.val);
                p1 = p1.next;
            } else {
                p2.next = new ListNode(head.val);
                p2 = p2.next;
            }
            head = head.next;
        }
        p1.next = b.next;
        return  a.next;
    }
}
```