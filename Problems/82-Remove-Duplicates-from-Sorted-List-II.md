# 82. Remove Duplicates from Sorted List II

Methods: Basic logic
Difficulty: Medium

**Medium**

7.5K

207

Companies

Given the `head` of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list*. Return *the linked list **sorted** as well*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

```
Input: head = [1,1,1,2,3]
Output: [2,3]

```

**Constraints:**

- The number of nodes in the list is in the range `[0, 300]`.
- `100 <= Node.val <= 100`
- The list is guaranteed to be **sorted** in ascending order.

```jsx
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode pN = new ListNode(-1);
        pN.next = head;
        ListNode p0 = pN;
        ListNode p1 = head.next;
        boolean dup = false; // 確認重複用

        while(p1 != null){
            if(head.val == p1.val){
                dup = true;
            }else{
                if(dup) {// 當前面有重複 有重新接節點
                    p0.next = p1;
                    dup = false;
                }
                else p0 = p0.next;
            }
            head = head.next;
            p1 = p1.next;
        }
        if(dup) p0.next = p1;// 避免[1,1]等情況 結尾有重複

        return pN.next;
    }
}
```