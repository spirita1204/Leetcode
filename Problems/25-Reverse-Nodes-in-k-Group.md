# 25. Reverse Nodes in k-Group

Methods: DFS
Difficulty: Hard

Hard

Topics

Companies

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return *the modified list*.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]

```

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 5000`
- `0 <= Node.val <= 1000`

**Follow-up:** Can you solve the problem in `O(1)` extra memory space?

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
    public ListNode reverseKGroup(ListNode head, int k) {
        // 先取得總長度 一次變更前k個 然後往後遞歸
        int l = 0;// 總長度
        ListNode cur = head;
        while (cur != null) {
            l++;
            cur = cur.next;
        }
        if (k > l) {
            return head;
        }
        cur = head;
        ListNode node = null;
        for (int i = 0; i < k; i++) {// 變換指標方向
            ListNode nxt = cur.next;
            cur.next = node;
            node = cur;// 3
            cur = nxt;// 4
        }
        head.next = reverseKGroup(cur, k);
        return node;
    }
}
```