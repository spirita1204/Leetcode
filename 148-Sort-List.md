# 148. Sort List

Methods: Sort
Difficulty: Medium

Given the `head` of a linked list, return *the list after sorting it in **ascending order***.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

```
Input: head = [4,2,1,3]
Output: [1,2,3,4]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

```
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]

```

**Example 3:**

```
Input: head = []
Output: []

```

**Constraints:**

- The number of nodes in the list is in the range `[0, 5 * 104]`.
- `105 <= Node.val <= 105`

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

Brute force

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
    public ListNode sortList(ListNode head) {
        if(head == null) return head;
        List<Integer> l = new ArrayList<>();

        while(head != null){
            l.add(head.val);
            head = head.next;
        }
        Collections.sort(l);
        ListNode res = new ListNode();
        ListNode ans = res;
        
        for(int i = 0; i < l.size(); i++ ){
            res.val = l.get(i);
            if(i != l.size()-1){
                res.next = new ListNode();
                res = res.next;
            }
        }
        return ans;
    }
}
```

高級 MERGE SORT 大神

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
public class Solution {
  public ListNode sortList(ListNode head) {
    if (head == null || head.next == null)
      return head;
        
    // step 1. cut the list to two halves
    ListNode prev = null, slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }
    
    prev.next = null;//將左節點作結
    
    // step 2. sort each half
    ListNode l1 = sortList(head);
    ListNode l2 = sortList(slow);
    
    // step 3. merge l1 and l2
    return merge(l1, l2);
  }
  
  ListNode merge(ListNode l1, ListNode l2) {
    ListNode l = new ListNode(0), p = l;
    
    while (l1 != null && l2 != null) {
      if (l1.val < l2.val) {
        p.next = l1;
        l1 = l1.next;
      } else {
        p.next = l2;
        l2 = l2.next;
      }
      p = p.next;
    }
    
    if (l1 != null)
      p.next = l1;
    
    if (l2 != null)
      p.next = l2;
    
    return l.next;
  }

}
```