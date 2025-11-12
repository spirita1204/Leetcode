# 2654. Minimum Number of Operations to Make All Array Elements Equal to 1  

  Methods: Greedy,Math </br> Difficulty: Medium </br> </br>You are given a **0-indexed** array `nums` consisiting of **positive** integers. You can do the following operation on the array **any** number of times:

- Select an index `i` such that `0 <= i < n - 1` and replace either of `nums[i]` or `nums[i+1]` with their gcd value.
Return *the ****minimum**** number of operations to make all elements of *`nums`* equal to *`1`. If it is impossible, return `-1`.

The gcd of two integers is the greatest common divisor of the two integers.

**Example 1:**

```plain text
Input: nums = [2,6,3,4]
Output: 4
Explanation: We can do the following operations:
- Choose index i = 2 and replace nums[2] with gcd(3,4) = 1. Now we have nums = [2,6,1,4].
- Choose index i = 1 and replace nums[1] with gcd(6,1) = 1. Now we have nums = [2,1,1,4].
- Choose index i = 0 and replace nums[0] with gcd(2,1) = 1. Now we have nums = [1,1,1,4].
- Choose index i = 2 and replace nums[3] with gcd(1,4) = 1. Now we have nums = [1,1,1,1].  
```

**Example 2:**

```plain text
Input: nums = [2,10,6,14]
Output: -1
Explanation: It can be shown that it is impossible to make all the elements equal to 1.
```

**Constraints:**

- `2 <= nums.length <= 50`
- `1 <= nums[i] <= 106`
```java
class Solution {
    public int minOperations(int[] nums) {
        int n = nums.length;
        int num1 = 0;
        int g = 0;// 全部共同gcd
        for (int x : nums) {
            if (x == 1) 
                num1++;
            g = gcd(g, x);
        }
        if (num1 > 0) 
            return n - num1;
        if (g > 1) // 無法變1
            return -1;

        int minLen = n;
        for (int i = 0; i < n; i++) {
            int currentGcd = 0;
            for (int j = i; j < n; j++) {// 找到最短子数组 gcd = 1
                currentGcd = gcd(currentGcd, nums[j]);
                if (currentGcd == 1) {
                    minLen = Math.min(minLen, j - i + 1);
                    break;
                }
            }
        }
        // minLen - 1 次操作可以把這個區間缩出一個 1
        // 剩下的 n - 1 個元素變成 1
        return minLen + n - 2;
    }

    private int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}
```

