# 525. Contiguous Array

Methods: Prefix Sum
Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Given a binary array `nums`, return *the maximum length of a contiguous subarray with an equal number of* `0` *and* `1`.

**Example 1:**

```
Input: nums = [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.

```

**Example 2:**

```
Input: nums = [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.

```java
class Solution {
    public int findMaxLength(int[] nums) {
        // prefix sum
        Map<Integer, Integer> hm = new HashMap<>();
        // nums [0, 1, 0, 1, 0, 0, 1, 0, 0, 0]
        // [-1,0,-1,0,-1,-2,-1,-2,-3,-4]
        int prefix = 0;
        int max = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == 1) prefix += 1;
            else prefix -= 1;   
            // case1 當前及滿足
            if(prefix == 0) max = Math.max(max, i + 1);
            // case2 找出可互補
            if(hm.containsKey(prefix)) max = Math.max(max, i - hm.get(prefix));
            // 避免覆蓋
            if(!hm.containsKey(prefix)) hm.put(prefix, i);
        }
        return max;
    }
}
```