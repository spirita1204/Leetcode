# 373. Find K Pairs with Smallest Sums

Data structure: Heap
Difficulty: Hard

Medium

Topics

Companies

You are given two integer arrays `nums1` and `nums2` sorted in **non-decreasing order** and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

Return *the* `k` *pairs* `(u1, v1), (u2, v2), ..., (uk, vk)` *with the smallest sums*.

**Example 1:**

```
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]

```

**Example 2:**

```
Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
Output: [[1,1],[1,1]]
Explanation: The first 2 pairs are returned from the sequence: [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]

```

**Constraints:**

- `1 <= nums1.length, nums2.length <= 105`
- `109 <= nums1[i], nums2[i] <= 109`
- `nums1` and `nums2` both are sorted in **non-decreasing order**.
- `1 <= k <= 104`
- `k <= nums1.length * nums2.length`

```java
class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        Queue<int[]> q = new PriorityQueue<>((a, b)->(a[0] + a[1] - b[0] - b[1]));
        List<List<Integer>> res = new ArrayList<>();

        for(int i = 0; i< nums1.length; i++) 
            q.offer(new int[]{ nums1[i], nums2[0], 0});// 第三位放nums2 index

        while(k-- > 0 && !q.isEmpty()) {
            int[] e = q.poll();
            res.add(Arrays.asList(e[0], e[1]));
            if(e[2] == nums2.length - 1) continue;
            q.offer(new int[]{e[0], nums2[e[2] + 1], e[2] + 1});
        }
        return res;
    }
}
```