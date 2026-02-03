# 3637. Trionic Array I  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given an integer array `nums` of length `n`.

An array is **trionic** if there exist indices `0 < p < q < n − 1` such that:

- `nums[0...p]` is **strictly** increasing,
- `nums[p...q]` is **strictly** decreasing,
- `nums[q...n − 1]` is **strictly** increasing.
Return `true` if `nums` is trionic, otherwise return `false`.

**Example 1:**

**Input:** nums = [1,3,5,4,2,6]

**Output:** true

**Explanation:**

Pick `p = 2`, `q = 4`:

- `nums[0...2] = [1, 3, 5]` is strictly increasing (`1 < 3 < 5`).
- `nums[2...4] = [5, 4, 2]` is strictly decreasing (`5 > 4 > 2`).
- `nums[4...5] = [2, 6]` is strictly increasing (`2 < 6`).
**Example 2:  **

**Input:** nums = [2,1,3]

**Output:** false

**Explanation:**

There is no way to pick `p` and `q` to form the required three segments.

**Constraints:**

- `3 <= n <= 100`
- `1000 <= nums[i] <= 1000`   
```java
class Solution {
    public boolean isTrionic(int[] nums) {
        int nowDir = 1;  
        int changeDirCnt = 0;
        for (int i = 1; i < nums.length; i++) {
            // 沒往上
            if (i == 1 && nums[i] - nums[i - 1] <= 0) {
                return false;
            } else if (nums[i] == nums[i - 1]) {
                return false;
            }
            if(nowDir == 1 && nums[i - 1] > nums[i]) {
                changeDirCnt++;
                nowDir = -1;
            } else if(nowDir == -1 && nums[i - 1] < nums[i]) {
                changeDirCnt++;
                nowDir = 1;
            }
        }
        return changeDirCnt == 2;
    }
} 
```

