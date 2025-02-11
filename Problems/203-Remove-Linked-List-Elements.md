# 203. Remove Linked List Elements

Methods: Pointer
Difficulty: Easy

**Easy**

7K

205

Companies

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return *the new head*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]

```

**Example 2:**

```
Input: head = [], val = 1
Output: []

```

**Example 3:**

```
Input: head = [7,7,7,7], val = 7
Output: []

```

**Constraints:**

- The number of nodes in the list is in the range `[0, 104]`.
- `1 <= Node.val <= 50`
- `0 <= val <= 50`

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
    public ListNode removeElements(ListNode head, int val) {
        if(head == null) return null;

        ListNode p0 = new ListNode(-1, head);// 指到第一位之前 輸出用
        ListNode p1 = p0;
        ListNode p2 = head.next;

        while(p2 != null) {
            if(head.val == val) p1.next = p2;
            else p1 = p1.next;
            
            head = head.next;
            p2 = p2.next;
        }
        
        if(head.val == val) p1.next = null;// 最後一位元處理

        return p0.next;
    }
}
```