# 3315. Construct the Minimum Bitwise Array II  

  Methods: Bitwise </br> Difficulty: Medium </br> </br>You are given an array `nums` consisting of `n` prime integers.

You need to construct an array `ans` of length `n`, such that, for each index `i`, the bitwise `OR` of `ans[i]` and `ans[i] + 1` is equal to `nums[i]`, i.e. `ans[i] OR (ans[i] + 1) == nums[i]`.

Additionally, you must **minimize** each value of `ans[i]` in the resulting array.

If it is *not possible* to find such a value for `ans[i]` that satisfies the **condition**, then set `ans[i] = -1`.

**Example 1:**

**Input:** nums = [2,3,5,7]

**Output:** [-1,1,4,3]

**Explanation:**

- For `i = 0`, as there is no value for `ans[0]` that satisfies `ans[0] OR (ans[0] + 1) = 2`, so `ans[0] = -1`.
- For `i = 1`, the smallest `ans[1]` that satisfies `ans[1] OR (ans[1] + 1) = 3` is `1`, because `1 OR (1 + 1) = 3`.
- For `i = 2`, the smallest `ans[2]` that satisfies `ans[2] OR (ans[2] + 1) = 5` is `4`, because `4 OR (4 + 1) = 5`.
- For `i = 3`, the smallest `ans[3]` that satisfies `ans[3] OR (ans[3] + 1) = 7` is `3`, because `3 OR (3 + 1) = 7`.
**Example 2:**

**Input:** nums = [11,13,31]

**Output:** [9,12,15]

**Explanation:**

- For `i = 0`, the smallest `ans[0]` that satisfies `ans[0] OR (ans[0] + 1) = 11` is `9`, because `9 OR (9 + 1) = 11`.
- For `i = 1`, the smallest `ans[1]` that satisfies `ans[1] OR (ans[1] + 1) = 13` is `12`, because `12 OR (12 + 1) = 13`.
- For `i = 2`, the smallest `ans[2]` that satisfies `ans[2] OR (ans[2] + 1) = 31` is `15`, because `15 OR (15 + 1) = 31`.
**Constraints:**

- `1 <= nums.length <= 100`
- `2 <= nums[i] <= 109`
- `nums[i]` is a prime number.
```java
class Solution {
    public int[] minBitwiseArray(List<Integer> nums) {
        int[] ans = new int[nums.size()];
        // nums[i] 的 右邊一定是一串連續的 1
        // 例如：7  = 111, 23 = 10111
        for (int i = 0; i < nums.size(); i++) {
            int num = nums.get(i);
            if (num == 2) {
                ans[i] = -1;
                continue;
            }
            int numCopy = num;
            int count = 0;
            // 計算右邊連續的 1
            while ((num & 1) == 1) {
                count++;
                num >>= 1;
            }
            // (count - 1) 對應的是 那串 1 裡「最高位的 1」                                    
            // 原本: 100111
            // 減掉:    100
            // 結果: 100011
            ans[i] = numCopy - (1 << (count - 1));
        } 

        return ans;
    }
}
```

