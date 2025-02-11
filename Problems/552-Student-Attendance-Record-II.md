# 552. Student Attendance Record II

Methods: DP
Difficulty: Hard

# Hard

Topics

Companies

An attendance record for a student can be represented as a string where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:

- `'A'`: Absent.
- `'L'`: Late.
- `'P'`: Present.

Any student is eligible for an attendance award if they meet **both** of the following criteria:

- The student was absent (`'A'`) for **strictly** fewer than 2 days **total**.
- The student was **never** late (`'L'`) for 3 or more **consecutive** days.

Given an integer `n`, return *the **number** of possible attendance records of length* `n` *that make a student eligible for an attendance award. The answer may be very large, so return it **modulo*** `109 + 7`.

**Example 1:**

```
Input: n = 2
Output: 8
Explanation: There are 8 records with length 2 that are eligible for an award:
"PP", "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" is not eligible because there are 2 absences (there need to be fewer than 2).

```

**Example 2:**

```
Input: n = 1
Output: 3

```

**Example 3:**

```
Input: n = 10101
Output: 183236316

```

**Constraints:**

- `1 <= n <= 105`

```java
class Solution {
    public int checkRecord(int n) {
        // 直觀 符合第一第二條件 = 2種狀態* 3種狀態 = 6
        // dp00[i] = for s[0:i] never a appeared 且 end with 0 L
        // dp01[i] = for s[0:i] never a appeared 且 end with 1 L
        // dp02[i] = for s[0:i] never a appeared 且 end with 2 L
        // dp10[i] = for s[0:i] a appeared once 且 end with 0 L
        // dp11[i] = for s[0:i] a appeared once 且 end with 1 L
        // dp12[i] = for s[0:i] a appeared once 且 end with 2 L

        long[] dp00 = new long[n + 1];
        long[] dp01 = new long[n + 1];
        long[] dp02 = new long[n + 1];
        long[] dp10 = new long[n + 1];
        long[] dp11 = new long[n + 1];
        long[] dp12 = new long[n + 1];
        int m = 1000000007;
        // 邊界條件
        dp00[0] = 1;
        dp01[0] = 0;
        dp02[0] = 0;
        dp10[0] = 0;
        dp11[0] = 0;
        dp12[0] = 0;

        for(int i = 1; i <= n; i++) {
            // dp01[i - 1]* 'P'
            dp00[i] = (dp00[i - 1]* 1 + dp01[i - 1]* 1 + dp02[i - 1]* 1) % m;
            dp01[i] = dp00[i - 1]* 1;
            dp02[i] = dp01[i - 1]* 1;
            // dp00[i- 1]* 'A' + dp01[i - 1]* 'A' + dp02[i - 1]* 'A' + dp10[i - 1]* 'P' + dp11[i - 1]* 'P' + dp12[i - 1]* 'P'
            dp10[i] = (dp00[i- 1]*1 + dp01[i - 1]* 1 + dp02[i - 1]* 1 
                        + dp10[i - 1]* 1 + dp11[i - 1]* 1 + dp12[i - 1]* 1) % m;
            dp11[i] = dp10[i - 1]* 1;
            dp12[i] = dp11[i - 1]* 1;
        }
        return (int)((dp00[n] + dp01[n] + dp02[n] + dp10[n] + dp11[n] + dp12[n]) % m); 
    }

        // // 第一要求
        // dp0[i] = for dp0[i - 1] never a appeared
        // dp1[i] = for dp1[i - 1] a appeared once
        // // 邊界條件
        // dp0[0] = 1;
        // dp1[0] = 0;
        
        // for(int i = 0; i<= n; i++) {
        //     dp0[i] = dp0[i - 1]* 2; // 最後一位可選L, P
        //     dp1[i] = dp1[i - 1]* 2 + dp0[i - 1]* 1 // 前面已出現一次(最後L, P) + 前面未出現過(最後A) 
        // }
        // return dp0[i] + dp1[i]; 
        // // 第二要求
        // dp0[i] = for dp0[i - 1] end with 0 L
        // dp1[i] = for dp1[i - 1] end with 1 L
        // dp2[i] = for dp2[i - 1] end with 2 L
        // // 邊界條件
        // dp0[0] = 1;
        // dp1[0] = 0;
        // dp2[0] = 0;
        
        // for(int i = 0; i<= n; i++) {
        //     dp0[i] = (dp0[i - 1] + dp1[i - 1] + dp2[i - 1])* 2// 三者情況都可以 相加(最後A, P)
        //     dp1[i] = dp0[i - 1]// 結尾0個L後面再接L
        //     dp2[i] = dp1[i - 1]*1// 結尾1個L後面再接L
        // }
        // return dp0[i] + dp1[i] + dp2[i];    
}
```