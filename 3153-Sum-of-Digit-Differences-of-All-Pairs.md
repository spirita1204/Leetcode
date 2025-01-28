# 3153. Sum of Digit Differences of All Pairs

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given an array `nums` consisting of **positive** integers where all integers have the **same** number of digits.

The **digit difference** between two integers is the *count* of different digits that are in the **same** position in the two integers.

Return the **sum** of the **digit differences** between **all** pairs of integers in `nums`.

**Example 1:**

**Input:** nums = [13,23,12]

**Output:** 4

**Explanation:**

We have the following:

- The digit difference between **1**3 and **2**3 is 1.
- The digit difference between 1**3** and 1**2** is 1.
- The digit difference between **23** and **12** is 2.

So the total sum of digit differences between all pairs of integers is `1 + 1 + 2 = 4`.

**Example 2:**

**Input:** nums = [10,10,10,10]

**Output:** 0

**Explanation:**

All the integers in the array are the same. So the total sum of digit differences between all pairs of integers will be 0.

**Constraints:**

- `2 <= nums.length <= 105`
- `1 <= nums[i] < 109`
- All integers in `nums` have the same number of digits.

```java
class Solution {
    public long sumDigitDifferences(int[] nums) {
        // 由 個位計算
        // 123 (2+2+2)/2 = 3     
        // 112 (2+2)/2 = 2
        // 1122 (4+4)/2 = 4 
        int length = nums.length;
        long sum = 0;
        while(nums[0] > 0) {
            long[] occur = new long[10];
            long sumInPosition = 0;
            // 記錄每一相同位子數字出現頻率
            for(int i = 0; i < nums.length; i++) {
                occur[nums[i] % 10]++;
                nums[i] /= 10;
            }
            // 計算同位置 pairs有多少diff
            for(long digit: occur) {
               sumInPosition += (digit * (length - digit));
            }
            // 個行 加回去給加總
            sum += (sumInPosition / 2);
        }
        return sum;
    }
}
```