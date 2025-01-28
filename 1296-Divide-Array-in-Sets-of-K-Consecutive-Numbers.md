# 1296. Divide Array in Sets of K Consecutive Numbers

Data structure: Hash Table
Difficulty: Medium
Similar: 846

Medium

Topics

Companies

Hint

Given an array of integers `nums` and a positive integer `k`, check whether it is possible to divide this array into sets of `k` consecutive numbers.

Return `true` *if it is possible*. ****Otherwise, return `false`.

**Example 1:**

```
Input: nums = [1,2,3,3,4,4,5,6], k = 4
Output: true
Explanation: Array can be divided into [1,2,3,4] and [3,4,5,6].

```

**Example 2:**

```
Input: nums = [3,2,1,2,3,4,3,4,5,9,10,11], k = 3
Output: true
Explanation: Array can be divided into [1,2,3] , [2,3,4] , [3,4,5] and [9,10,11].

```

**Example 3:**

```
Input: nums = [1,2,3,4], k = 3
Output: false
Explanation: Each array should be divided in subarrays of size 3.

```

**Constraints:**

- `1 <= k <= nums.length <= 105`
- `1 <= nums[i] <= 109`

**Note:**

This question is the same as 846:

[https://leetcode.com/problems/hand-of-straights/](https://leetcode.com/problems/hand-of-straights/)

```java
class Solution {
    public boolean isPossibleDivide(int[] nums, int k) {
        if (nums.length % k != 0)
            return false;
        Arrays.sort(nums);
        // [1,2,2,3,3,4,6,7,8]
        Map<Integer, Integer> hm = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            hm.put(nums[i], hm.getOrDefault(nums[i], 0) + 1);
        }
        for (int i = 0; i < nums.length; i++) {
            if (hm.get(nums[i]) > 0) {
                for (int j = 0; j < k; j++) {
                    if (hm.get(nums[i] + j) == null || hm.get(nums[i] + j) == 0)
                        return false;
                    else
                        hm.put(nums[i] + j, hm.get(nums[i] + j) - 1);
                }
            }
        }
        return true;
    }
}
```