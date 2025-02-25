# 1524. Number of Sub-arrays With Odd Sum  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>Given an array of integers `arr`, return *the number of subarrays with an ****odd**** sum*.

Since the answer can be very large, return it modulo `109 + 7`.

**Example 1:**

```plain text
Input: arr = [1,3,5]
Output: 4
Explanation: All subarrays are [[1],[1,3],[1,3,5],[3],[3,5],[5]]
All sub-arrays sum are [1,4,9,3,8,5].
Odd sums are [1,9,3,5] so the answer is 4.

```

**Example 2:**

```plain text
Input: arr = [2,4,6]
Output: 0
Explanation: All subarrays are [[2],[2,4],[2,4,6],[4],[4,6],[6]]
All sub-arrays sum are [2,6,12,4,10,6].
All sub-arrays have even sum and the answer is 0.

```

**Example 3:**

```plain text
Input: arr = [1,2,3,4,5,6,7]
Output: 16

```

**Constraints:**

- `1 <= arr.length <= 105`
- `1 <= arr[i] <= 100`
```java
class Solution {
    public int numOfSubarrays(int[] arr) {
        int MOD = 1000000007;
        // prefix sum 偶奇 奇偶
        int odd = 0; // 記錄前綴和為奇數次數
        int even = 1; // 記錄前綴和為偶數次數
        int prefix = 0;
        int res = 0;
        for(int i = 0; i < arr.length; i++) {
            prefix += arr[i];
            if (prefix % 2 == 1) {// odd
                res = (res + even) % MOD;
                odd++;
            } else {// even
                res = (res + odd) % MOD;
                even++;
            }
        }
        return res;
    }
}
```

