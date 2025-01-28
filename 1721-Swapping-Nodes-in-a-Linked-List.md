# 1721. Swapping Nodes in a Linked List

Methods: Pointer
Difficulty: Medium

**Medium**

4.4K

146

Companies

You are given the `head` of a linked list, and an integer `k`.

Return *the head of the linked list after **swapping** the values of the* `kth` *node from the beginning and the* `kth` *node from the end (the list is **1-indexed**).*

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/21/linked1.jpg](https://assets.leetcode.com/uploads/2020/09/21/linked1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [1,4,3,2,5]

```

**Example 2:**

```
Input: head = [7,9,6,6,7,8,3,0,9,5], k = 5
Output: [7,9,6,6,8,7,3,0,9,5]

```

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 105`
- `0 <= Node.val <= 100`

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
    public ListNode swapNodes(ListNode head, int k) {
        ListNode fast = head;
        ListNode slow = head;
        ListNode first = head, second = head;
        
		// Put fast (k-1) nodes after slow
        for(int i = 0; i < k - 1; ++i)
            fast = fast.next;
		// Save the node for swapping
        first = fast;
		// Move until the end of the list
        while(fast.next != null) {
			slow = slow.next;
            fast = fast.next;
        }
        second = slow;
		// Swap values
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
        
        return head;
        /*
        if(head == null) return null;
        ListNode p = head;// 算長度
        ListNode p1 = head;// 遍歷用
        ListNode p2 = null;
        int length = 0;
        
        while(p != null) {
            p = p.next;
            length++;
        }
        int j = length - k + 1;// 要交換點
        
        if(j == k) return head;// 不用置換
        while((j >= 0 || k >= 0) && p1 != null) {
            j--;
            k--;
       
            if(p2 != null && j <= 0 && k <= 0) {
                int tmp = p2.val;
                p2.val = p1.val;
                p1.val = tmp;
                break;
            }
            if(j == 0 || k == 0) p2 = p1;
   
            p1 = p1.next;
        }
        return head;
        */
    }
}
```