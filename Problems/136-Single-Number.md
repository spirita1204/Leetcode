# 136. Single Number  

  Methods: Bitwise </br> Difficulty: Easy </br> </br>Given a **non-empty** array of integers `nums`, every element appears *twice* except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Example 1:**

```plain text
Input: nums = [2,2,1]
Output: 1

```

**Example 2:**

```plain text
Input: nums = [4,1,2,1,2]
Output: 4

```

**Example 3:**

```plain text
Input: nums = [1]
Output: 1

```

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `3 * 104 <= nums[i] <= 3 * 104`
- Each element in the array appears twice except for one element which appears only once.
```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for(int i = 0;i< nums.length;i++){
            //自己xor自己會抵消
            //((2^2)^(1^1)^(4^4)^(5)) => (0^0^0^5) => 5.
            result ^= nums[i];
        }    
        return result;
    }
}
```

