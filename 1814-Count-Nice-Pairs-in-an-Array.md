# 1814. Count Nice Pairs in an Array

Data structure: Hash Table
Difficulty: Medium
Similar: 2364

Medium

You are given an array `nums` that consists of non-negative integers. Let us define `rev(x)` as the reverse of the non-negative integer `x`. For example, `rev(123) = 321`, and `rev(120) = 21`. A pair of indices `(i, j)` is **nice** if it satisfies all of the following conditions:

- `0 <= i < j < nums.length`
- `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])`

Return *the number of nice pairs of indices*. Since that number can be too large, return it **modulo** `109 + 7`.

**Example 1:**

```
Input: nums = [42,11,1,97]
Output: 2
Explanation: The two pairs are:
 - (0,3) : 42 + rev(97) = 42 + 79 = 121, 97 + rev(42) = 97 + 24 = 121.
 - (1,2) : 11 + rev(1) = 11 + 1 = 12, 1 + rev(11) = 1 + 11 = 12.

```

**Example 2:**

```
Input: nums = [13,10,35,24,76]
Output: 4

```

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`

```java
class Solution {
    public int countNicePairs(int[] nums) {
        // nums[i] + rev(nums[j]) == nums[j] + rev(nums[i]) 等同於
        // nums[i] - rev(nums[i]) == nums[j] - rev(nums[j])
        Map<Integer, Integer> hm = new HashMap<>();
        int res = 0;

        for(int i = 0; i < nums.length; i++) {
           int prev = hm.getOrDefault(nums[i] - rev(nums[i]), 0);
           res += prev;
           hm.put(nums[i] - rev(nums[i]), prev + 1);
           res %= 1000000007;
        }
        return res;
    }

    private int rev(int i) {
        int reverse = 0;
        while (i != 0) {
            int r = i % 10;
            reverse = reverse * 10 + r;
            i /= 10;
        }
        return reverse;
    }
}
```