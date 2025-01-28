# 206. Reverse Linked List

Methods: Basic logic
Difficulty: Easy

**Easy**

17.2K

305

Companies

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
Input: head = [1,2]
Output: [2,1]

```

**Example 3:**

```
Input: head = []
Output: []

```

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `5000 <= Node.val <= 5000`

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

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
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode p1 = head;
        while(p1.next != null){//找到尾
            p1 = p1.next;
        }
        ListNode tail = p1;
        recursion(head);
        return tail;
    }
    public ListNode recursion(ListNode p1) {
        if(p1.next == null) return p1;
        ListNode rev = recursion(p1.next);//後面節點
        p1.next = null;
        rev.next = p1;//與前面交換
        rev = rev.next;
        return rev;
    }
}
```