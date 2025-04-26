# 1749. Maximum Absolute Sum of Any Subarray  

  Methods: Prefix Sum,Array </br> Difficulty: Medium </br> </br>You are given an integer array `nums`. The **absolute sum** of a subarray `[numsl, numsl+1, ..., numsr-1, numsr]` is `abs(numsl + numsl+1 + ... + numsr-1 + numsr)`.

Return *the ****maximum**** absolute sum of any ****(possibly empty)**** subarray of *`nums`.

Note that `abs(x)` is defined as follows:

- If `x` is a negative integer, then `abs(x) = -x`.
- If `x` is a non-negative integer, then `abs(x) = x`.
**Example 1:**

```plain text
Input: nums = [1,-3,2,3,-4]
Output: 5
Explanation: The subarray [2,3] has absolute sum = abs(2+3) = abs(5) = 5.
```

**Example 2:**

```plain text
Input: nums = [2,-5,1,-4,3,-2]
Output: 8
Explanation: The subarray [-5,1,-4] has absolute sum = abs(-5+1-4) = abs(-8) = 8.
```

**Constraints:**

- `1 <= nums.length <= 105`
- `104 <= nums[i] <= 104`
### Prefix Sum

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {
        int prefix = 0;
        int minPrefix = 0, maxPrefix = 0;
        int res = 0;
        
        for (int i = 0; i < nums.length; i++) {
            prefix += nums[i];
            // 考慮正負
            res = Math.max(res, Math.abs(prefix - minPrefix));
            res = Math.max(res, Math.abs(prefix - maxPrefix));
            // 找最大最小prefix
            minPrefix = Math.min(minPrefix, prefix);
            maxPrefix = Math.max(maxPrefix, prefix);
        }
        return res;
    
    }
}
```

最優解

```java
class Solution {
    public int maxAbsoluteSum(int[] a) {
        int len = a.length;
        int sum = 0;
        int min = 0, max = 0;

        for (int i = 0; i < len; i++) {
            sum = sum + a[i];
            if (sum > max)
                max = sum;
            if (sum < min)
                min = sum;
        }
        return max - min;
    }
}  
```





