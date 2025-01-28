# 974. Subarray Sums Divisible by K

Methods: Prefix Sum
Data structure: Hash Table, Set
Difficulty: Medium

Medium

Topics

Companies

Given an integer array `nums` and an integer `k`, return *the number of non-empty **subarrays** that have a sum divisible by* `k`.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

```
Input: nums = [4,5,0,-2,-3,1], k = 5
Output: 7
Explanation: There are 7 subarrays with a sum divisible by k = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]

```

**Example 2:**

```
Input: nums = [5], k = 9
Output: 0

```

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `104 <= nums[i] <= 104`
- `2 <= k <= 104`

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int n = nums.length;
        Map<Integer, Integer> hm = new HashMap<>();
        int res = 0;
        int prefix = 0;
        // prefix sum
        for(int i = 0; i < n; i++) {
            prefix += nums[i];
            prefix %= k;
            // case1 當前prefix sum 即符合要求
            if(prefix == 0) res++;
            // case2 餘數有相同
            if(hm.containsKey(prefix)) res += hm.get(prefix);
            // case3 因為有負數 餘數可以跟互補的組合 滿足整除k ex: k = 2, prefix = 1, key = -1
            if(hm.containsKey(prefix + k)) res += hm.get(prefix + k);
            if(hm.containsKey(prefix - k)) res += hm.get(prefix - k);
            // 避免覆蓋
            hm.put(prefix, hm.getOrDefault(prefix, 0) + 1);
        }
        return res;
    }
}
```