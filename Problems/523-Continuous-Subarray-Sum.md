# 523. Continuous Subarray Sum  

  Methods: Prefix Sum </br> Data Structure: Hash Table </br> Difficulty: Medium </br> </br>Given an integer array nums and an integer k, return `true` *if *`nums`* has a ****good subarray**** or *`false`* otherwise*.

A **good subarray** is a subarray where:

- its length is **at least two**, and
- the sum of the elements of the subarray is a multiple of `k`.
**Note** that:

- A **subarray** is a contiguous part of the array.
- An integer `x` is a multiple of `k` if there exists an integer `n` such that `x = n * k`. `0` is **always** a multiple of `k`.
**Example 1:**

```plain text
Input: nums = [23,2,4,6,7], k = 6
Output: true
Explanation: [2, 4] is a continuous subarray of size 2 whose elements sum up to 6.
```

**Example 2:**

```plain text
Input: nums = [23,2,6,4,7], k = 6
Output: true
Explanation: [23, 2, 6, 4, 7] is an continuous subarray of size 5 whose elements sum up to 42.
42 is a multiple of 6 because 42 = 7 * 6 and 7 is an integer.
```

**Example 3:**

```plain text
Input: nums = [23,2,6,4,7], k = 13
Output: false
```

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`
- `0 <= sum(nums[i]) <= 231 - 1`
- `1 <= k <= 231 - 1`
```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        // prefix sum 求任意區間和sum[i, j] = prefix[j] - prefix[i];
        Map<Integer, Integer> hm = new HashMap<>();
        int sum = 0;

        for(int i = 0; i < nums.length; i++) {
            sum += nums[i];
            sum %= k;
            // case1 : prefix sum 即符合
            if(sum == 0 && i > 0) return true;
            // case2 : 當前餘數可以在hm中找到相同 ->代表相減可以抵銷->整除k
            if(hm.containsKey(sum) && i - hm.get(sum) > 1) return true;
            // 避免覆蓋
            if (!hm.containsKey(sum)) hm.put(sum, i); 
        }
        return false;
    }
}
```

