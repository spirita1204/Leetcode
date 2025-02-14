# 3217. Delete Nodes From Linked List Present in Array

Methods: Basic logic
Data structure: Set
Difficulty: Medium

You are given an array of integers `nums` and the `head` of a linked list. Return the `head` of the modified linked list after **removing** all nodes from the linked list that have a value that exists in `nums`.

**Example 1:**

**Input:** nums = [1,2,3], head = [1,2,3,4,5]

**Output:** [4,5]

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample0.png](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample0.png)

Remove the nodes with values 1, 2, and 3.

**Example 2:**

**Input:** nums = [1], head = [1,2,1,2,1,2]

**Output:** [2,2,2]

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample1.png](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample1.png)

Remove the nodes with value 1.

**Example 3:**

**Input:** nums = [5], head = [1,2,3,4]

**Output:** [1,2,3,4]

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample2.png](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample2.png)

No node has value 5.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`
- All elements in `nums` are unique.
- The number of nodes in the given list is in the range `[1, 105]`.
- `1 <= Node.val <= 105`
- The input is generated such that there is at least one node in the linked list that has a value not present in `nums`.

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
    public ListNode modifiedList(int[] nums, ListNode head) {
        Set<Integer> s = new HashSet<>();
        for(int i: nums)
            s.add(i);
        // 應除開頭
        while(head != null) {
            if(s.contains(head.val)) {
                head = head.next;
            } else break;
        }
        ListNode res = head;
        ListNode p2 = head;
        // 清除之後
        head = head.next;// 當前一定不contains
        while(head != null) {
            if(s.contains(head.val)) {
                head = head.next;
                p2.next = head;//跳過當前
            } else {
                head = head.next;
                p2 = p2.next;
            }
        }
        return res;
    }
}
```