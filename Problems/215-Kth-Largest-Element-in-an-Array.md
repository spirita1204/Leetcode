# 215. Kth Largest Element in an Array

Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

Given an integer array `nums` and an integer `k`, return *the* `kth` *largest element in the array*.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

**Example 1:**

```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5

```

**Example 2:**

```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4

```

**Constraints:**

- `1 <= k <= nums.length <= 105`
- `104 <= nums[i] <= 104`

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Queue<Integer> q = new PriorityQueue<>((a, b)-> b - a);
        for(int i: nums) {
            q.offer(i);
        }
        while(k-- > 1) {
            q.poll();
        }
        return q.poll();
    }
}
```