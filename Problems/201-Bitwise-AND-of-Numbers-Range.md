# 201. Bitwise AND of Numbers Range  

  Methods: Bitwise </br> Difficulty: Medium </br> </br>**Medium**

2.8K

197

Companies

Given two integers `left` and `right` that represent the range `[left, right]`, return *the bitwise AND of all numbers in this range, inclusive*.

**Example 1:**

```plain text
Input: left = 5, right = 7
Output: 4

```

**Example 2:**

```plain text
Input: left = 0, right = 0
Output: 0

```

**Example 3:**

```plain text
Input: left = 1, right = 2147483647
Output: 0

```

**Constraints:**

- `0 <= left <= right <= 231 - 1`
```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        // 最後一位一定 0
        // Bitwise-AND of any two numbers will always produce a number less than or equal to the smaller number.
        // https://leetcode.com/problems/bitwise-and-of-numbers-range/solutions/593317/simple-3-line-java-solution-faster-than-100/
        while(right > left)
            right = right & right- 1;

        return right;
    }
}
```

