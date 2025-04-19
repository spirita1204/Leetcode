# 2563. Count the Number of Fair Pairs  

  Methods: Binary Search </br> Difficulty: Medium </br> </br>Given a **0-indexed** integer array `nums` of size `n` and two integers `lower` and `upper`, return *the number of fair pairs*.

A pair `(i, j)` is **fair **if:

- `0 <= i < j < n`, and 
- `lower <= nums[i] + nums[j] <= upper`
**Example 1:**

```plain text
Input: nums = [0,1,7,4,4,5], lower = 3, upper = 6
Output: 6
Explanation: There are 6 fair pairs: (0,3), (0,4), (0,5), (1,3), (1,4), and (1,5).
```

**Example 2:**

```plain text
Input: nums = [1,7,9,2,5], lower = 11, upper = 11
Output: 1
Explanation: There is a single fair pair: (2,3).
```

**Constraints:**

- `1 <= nums.length <= 105`
- `nums.length == n`
- `109 <= nums[i] <= 109`
- `109 <= lower <= upper <= 109`
```java
class Solution {
    public long countFairPairs(int[] nums, int lower, int upper) {
        long res = 0;
        int len = nums.length;

        Arrays.sort(nums);
        // 1 2 5 7 9

        for (int i = 0; i < len - 1; i++) {
            int min = 0;
            int max = 0;

            int left = i;
            int right = len - 1;
            // 找最小
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[i] + nums[mid] < lower) {
                    left = mid + 1;
                } else if (nums[i] + nums[mid] >= lower) {
                    right = mid - 1;
                }
            }
            min = left;//
            left = i;
            right = len - 1;
            // 找最大
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[i] + nums[mid] <= upper) {
                    left = mid + 1;
                } else if (nums[i] + nums[mid] > upper) {
                    right = mid - 1;
                }
            }
            max = left;//
            // min != max 避免負數
            res += (min == i && min != max) ? (max - min - 1) : (max - min);
        }
        return res;
    }
}
```

