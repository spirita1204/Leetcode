# 2537. Count the Number of Good Subarrays  

  Methods: Sliding Window </br> Data Structure: Hash Table </br> Difficulty: Medium </br> </br>Given an integer array `nums` and an integer `k`, return *the number of ****good**** subarrays of* `nums`.

A subarray `arr` is **good** if there are **at least **`k` pairs of indices `(i, j)` such that `i < j` and `arr[i] == arr[j]`.

A **subarray** is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

```plain text
Input: nums = [1,1,1,1,1], k = 10
Output: 1
Explanation: The only good subarray is the array nums itself.
```

**Example 2:**

```plain text
Input: nums = [3,1,4,3,2,2,4], k = 2
Output: 4
Explanation: There are 4 different good subarrays:
- [3,1,4,3,2,2] that has 2 pairs.
- [3,1,4,3,2,2,4] that has 3 pairs.
- [1,4,3,2,2,4] that has 2 pairs.
- [4,3,2,2,4] that has 2 pairs.
```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i], k <= 109`
```java
class Solution {
    public long countGood(int[] nums, int k) {
        long res = 0;
        Map<Integer, Integer> count = new HashMap<>();
        int i = 0;
        for (int j = 0; j < nums.length; j++) {
            k -= count.getOrDefault(nums[j], 0);
            count.put(nums[j], count.getOrDefault(nums[j], 0) + 1);

            while (k <= 0) {// 左指標右移
                count.put(nums[i], count.get(nums[i]) - 1);
                k += count.get(nums[i]);
                i++;
            }
            res += i;
        }
        return res;
    }
}
```

