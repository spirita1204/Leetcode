# 143. Reorder List

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

You are given the head of a singly linked-list. The list can be represented as:

```
L0 → L1 → … → Ln - 1 → Ln
```

*Reorder the list to be on the following form:*

```
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …

```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

```
Input: head = [1,2,3,4]
Output: [1,4,2,3]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/03/09/reorder2-linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/09/reorder2-linked-list.jpg)

```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]

```

**Constraints:**

- The number of nodes in the list is in the range `[1, 5 * 104]`.
- `1 <= Node.val <= 1000`

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
    public void reorderList(ListNode head) {
        if(head == null || head.next == null) return;

        ListNode p1 = head;// 中間
        ListNode p2 = head;// 尾部
        ListNode inter = head;// 交叉組合用
        ListNode keep = head;// 

        while (p2.next != null && p2.next.next != null) {// 找到尾
            p1 = p1.next;
            p2 = p2.next.next;
        }
        while(p2.next != null) {
            p2 = p2.next;
        }
        ListNode tail = p2;
        ListNode p1Next = p1.next;
        p1.next = null;
        recursion(p1Next);// 將一半之後反轉
        
        // 交叉組合
        while(tail != null) {// inter tail
            ListNode interNext = inter.next;// 先記錄左串的下一個
            keep.next = tail;// 將其串接反轉第一個
            keep = keep.next;
            tail = tail.next;// 反轉移位到下個
            inter = interNext;// 左串移到下個
            keep.next = inter;
            keep = keep.next;
        }
    }

    private ListNode recursion(ListNode p1) {
        if (p1.next == null)
            return p1;
        ListNode rev = recursion(p1.next);// 後面節點
        p1.next = null;
        rev.next = p1;// 與前面交換
        rev = rev.next;
        return rev;
    }
}
```