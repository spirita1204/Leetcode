# 92. Reverse Linked List II

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return *the reversed list*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]

```

**Example 2:**

```
Input: head = [5], left = 1, right = 1
Output: [5]

```

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= n <= 500`
- `500 <= Node.val <= 500`
- `1 <= left <= right <= n`

**Follow up:**

Could you do it in one pass?

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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if(head == null || head.next == null) return head;
        ListNode prevHead = new ListNode();
        prevHead.next = head;

        ListNode p1 = prevHead;
        for(int i = 1; i < left; i++) {
            p1 = p1.next;// 找到交換之前一節點
        }
        ListNode p2 = prevHead;
        for(int i = 0; i <= right; i++) {
            p2 = p2.next;// 找到交換後一節點
        }
        ListNode tail  = recursion(p1.next, right - left, p1);
        tail.next = p2;// 將反轉完尾巴和剩下相接

        return prevHead.next;
    }
    private ListNode recursion(ListNode p1, int step, ListNode pre) {
        if(step == 0) {
            pre.next = p1;// 1 -> 4// 將頭接到反轉首
            return p1;
        }
        ListNode rev = recursion(p1.next, step - 1, pre);//後面節點
        p1.next = null;
        rev.next = p1;//與前面交換
        rev = rev.next;
        return rev;
    }
}
```