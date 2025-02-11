# 930. Binary Subarrays With Sum

Methods: Pointer, Prefix Sum
Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Given a binary array `nums` and an integer `goal`, return *the number of non-empty **subarrays** with a sum* `goal`.

A **subarray** is a contiguous part of the array.

**Example 1:**

```
Input: nums = [1,0,1,0,1], goal = 2
Output: 4
Explanation: The 4 subarrays are bolded and underlined below:
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]

```

**Example 2:**

```
Input: nums = [0,0,0,0,0], goal = 0
Output: 15

```

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `nums[i]` is either `0` or `1`.
- `0 <= goal <= nums.length`

```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int goal) {
        int res = 0;
        int prefixSum = 0;
        Map<Integer, Integer> hm = new HashMap();// value存 幾種
        hm.put(0, 1);// 定義剛好等於goal 情況
        // sum[i:j] = prefix[j] - prefix[i - 1] = s
        // prefix[i - 1] = prefix[j] - s
        for (int i = 0; i < nums.length; i++) {
            prefixSum += nums[i];

            if(hm.containsKey(prefixSum - goal)) 
                res += hm.get(prefixSum - goal);
            
            hm.put(prefixSum, hm.getOrDefault(prefixSum, 0) + 1);
        }
        return res;
    }
}
```

Sliding Window

```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int goal) {
        // Sliding Window
        int res = 0, sum = 0, p1 = 0;
        for (int p2 = 0; p2 < nums.length; p2++) {
            sum += nums[p2];
            while (p1 < p2 && sum > goal) {
                sum -= nums[p1];
                p1++;
            }
            if (sum < goal) continue;
            // 剛好符合
            if (sum == goal) res++;
            // 前後如果都0可去掉 代表一種
            for (int j = p1; j < p2 && nums[j] == 0; j++) {
                res++;
            }
        }
        return res;
    }
}
```