# 234. Palindrome Linked List

Methods: Pointer
Difficulty: Easy

Easy

Topics

Companies

Given the `head` of a singly linked list, return `true` *if it is a*

*palindrome*

*or*

```
false
```

*otherwise*

.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false

```

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

**Follow up:**

Could you do it in

```
O(n)
```

time and

```
O(1)
```

space?

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
    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null) return true;

        ListNode p1 = head;
        ListNode p2 = head;
        Stack<Integer> st = new Stack<>();
        
        while(p2 != null && p2.next != null) {
            st.push(p1.val);
            p1 = p1.next;
            p2 = p2.next.next;
        }
        if(p2 != null && p2.next == null) {// 單數
            p1 = p1.next;
        }
        while(p1 != null) {
            int top = st.pop();
            if(top != p1.val) return false;
            p1 = p1.next;
        }
        return true;
    }
}
```