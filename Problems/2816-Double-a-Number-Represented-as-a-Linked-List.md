# 2816. Double a Number Represented as a Linked List

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given the `head` of a **non-empty** linked list representing a non-negative integer without leading zeroes.

Return *the* `head` *of the linked list after **doubling** it*.

**Example 1:**

![https://assets.leetcode.com/uploads/2023/05/28/example.png](https://assets.leetcode.com/uploads/2023/05/28/example.png)

```
Input: head = [1,8,9]
Output: [3,7,8]
Explanation: The figure above corresponds to the given linked list which represents the number 189. Hence, the returned linked list represents the number 189 * 2 = 378.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2023/05/28/example2.png](https://assets.leetcode.com/uploads/2023/05/28/example2.png)

```
Input: head = [9,9,9]
Output: [1,9,9,8]
Explanation: The figure above corresponds to the given linked list which represents the number 999. Hence, the returned linked list reprersents the number 999 * 2 = 1998.

```

**Constraints:**

- The number of nodes in the list is in the range `[1, 104]`
- `0 <= Node.val <= 9`
- The input is generated such that the list represents a number that does not have leading zeros, except the number `0` itself.

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
    public ListNode doubleIt(ListNode head) {
        int t = multiply(head);
        if (t != 0)// 當最前面易位
            head = new ListNode(t, head);
        return head;
    }

    private int multiply(ListNode head) {
        if (head == null)
            return 0;
        int t = head.val * 2 + multiply(head.next);
        head.val = t % 10;// 給定當前
        return t / 10;// 回傳易位
    }
}
```