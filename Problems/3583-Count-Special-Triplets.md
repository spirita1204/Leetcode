# 3583. Count Special Triplets  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given an integer array `nums`.

A **special triplet** is defined as a triplet of indices `(i, j, k)` such that:

- `0 <= i < j < k < n`, where `n = nums.length`
- `nums[i] == nums[j] * 2`
- `nums[k] == nums[j] * 2`
Return the total number of **special triplets** in the array.

Since the answer may be large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** nums = [6,3,6]

**Output:** 1

**Explanation:**

The only special triplet is `(i, j, k) = (0, 1, 2)`, where:

- `nums[0] = 6`, `nums[1] = 3`, `nums[2] = 6`
- `nums[0] = nums[1] * 2 = 3 * 2 = 6`
- `nums[2] = nums[1] * 2 = 3 * 2 = 6`
**Example 2:**

**Input:** nums = [0,1,0,0]

**Output:** 1

**Explanation:**

The only special triplet is `(i, j, k) = (0, 2, 3)`, where:

- `nums[0] = 0`, `nums[2] = 0`, `nums[3] = 0`
- `nums[0] = nums[2] * 2 = 0 * 2 = 0`
- `nums[3] = nums[2] * 2 = 0 * 2 = 0`
**Example 3:**

**Input:** nums = [8,4,2,8,4]

**Output:** 2

**Explanation:**

There are exactly two special triplets:

- `(i, j, k) = (0, 1, 3)`
- `(i, j, k) = (1, 2, 4)`
**Constraints:**

- `3 <= n == nums.length <= 105`
- `0 <= nums[i] <= 105`
```java
class Solution {
    final static int mod = (int) 1e9 + 7, M = (int) 1e5 + 1;

    public int specialTriplets(int[] nums) {
        // 對於每個 j：
        // 左邊有多少個 2x  
        // 右邊有多少個 2x  
        // 兩者相乘 = 貢獻到答案的 triplets
        int n = nums.length;
        int[] freq = new int[M];
        int[] prev = new int[M];
        for (int x : nums)
            freq[x]++;

        long cnt = 0;
        prev[nums[0]]++;

        for (int i = 1; i < n - 1; i++) {
            int x = nums[i], x2 = x << 1;
            if (x2 < M)
                cnt += (long) prev[x2] * (freq[x2] - prev[x2] - (x == 0 ? 1 : 0));
            prev[x]++;
        }
        return (int) (cnt % mod);
    }
}
```



