# 260. Single Number III  

  Methods: Bitwise </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

Given an integer array `nums`, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in **any order**.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

**Example 1:**

```plain text
Input: nums = [1,2,1,3,2,5]
Output: [3,5]
Explanation: [5, 3] is also a valid answer.

```

**Example 2:**

```plain text
Input: nums = [-1,0]
Output: [-1,0]

```

**Example 3:**

```plain text
Input: nums = [0,1]
Output: [1,0]

```

**Constraints:**

- `2 <= nums.length <= 3 * 104`
- `231 <= nums[i] <= 231 - 1`
- Each integer in `nums` will appear twice, only two integers will appear once.
```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int[] res = new int[2];
        int result = 0;
        // xor 位 = 1 代表該位a, b不相同, 0代表a, b 相同 
        // => 透過某一位xor = 1 分成兩個group a, b會在不同邊 => 變回第一道題
        // 3 = 011
        // 5 = 101
        // xor 110 = 6
        for(int n: nums) {
            result ^= n;
        }
        // 6 & -6 = 最低有效位（lowest set bit） key point
        // 0110 & 1010 (反轉+1)
        result &= -result;
        for(int num: nums) {
            if((num & result) == 0) {// 分兩個group 分別作找a, b 
                res[0] ^= num;
            } else {
                res[1] ^= num;
            }
        }
        return res;
    }
}
```

