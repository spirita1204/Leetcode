# 61. Rotate List

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

```
Input: head = [0,1,2], k = 4
Output: [2,0,1]

```

**Constraints:**

- The number of nodes in the list is in the range `[0, 500]`.
- `100 <= Node.val <= 100`
- `0 <= k <= 2 * 109`

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
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null) return null;
        int length = 0;
        ListNode lead = head;// p指到頭
        ListNode tail = null;

        while(head != null) {// 讓ll 變成circular linked list
            length++;
            if(head.next == null) {// 到尾
                head.next = lead;
                break;
            }else {
                head = head.next;
            }
        }
        int needMove = length - Math.abs(k % length) + 1;// 需移動幾次
        
        while(needMove-- >= 0) {
            if(needMove == 0) {
                tail.next = null;
                break;
            }
            tail = lead;
            lead = lead.next;
        }
        return lead;
    }
}
```