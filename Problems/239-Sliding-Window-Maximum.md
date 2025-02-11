# 239. Sliding Window Maximum

Data structure: Heap
Difficulty: Hard

Hard

Topics

Companies

Hint

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return *the max sliding window*.

**Example 1:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  73
 1 [3  -1  -3] 5  3  6  73
 1  3 [-1  -3  5] 3  6  7 5
 1  3  -1 [-3  5  3] 6  75
 1  3  -1  -3 [5  3  6] 76
 1  3  -1  -3  5 [3  6  7]7
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]

```

**Constraints:**

- `1 <= nums.length <= 105`
- `104 <= nums[i] <= 104`
- `1 <= k <= nums.length`

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> nums[b] - nums[a]);// 存索引 nums大到小
        int len = nums.length;
        int[] res = new int[len - k + 1];
        int idx = 0;
        
        for (int i = 0; i < len; i++) {
            while (pq.size() > 0 && pq.peek() <= i - k) {// 索引不在範圍 poll
                pq.poll();
            }
            pq.offer(i);
            if (i - k + 1 >= 0) {// 當達到範圍k range 計算最大
                res[idx++] = nums[pq.peek()];
            }
        }
        return res;
    }
}
```