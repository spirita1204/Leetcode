# 2197. Replace Non-Coprime Numbers in Array  

  Data Structure: Stack </br> Difficulty: Hard </br> </br>You are given an array of integers `nums`. Perform the following steps:  

1. Find **any** two **adjacent** numbers in `nums` that are **non-coprime**.
1. If no such numbers are found, **stop** the process.
1. Otherwise, delete the two numbers and **replace** them with their **LCM (Least Common Multiple)**.
1. **Repeat** this process as long as you keep finding two adjacent non-coprime numbers.
Return *the ****final**** modified array.* It can be shown that replacing adjacent non-coprime numbers in **any** arbitrary order will lead to the same result.

The test cases are generated such that the values in the final array are **less than or equal** to `108`.

Two values `x` and `y` are **non-coprime** if `GCD(x, y) > 1` where `GCD(x, y)` is the **Greatest Common Divisor** of `x` and `y`.   

**Example 1:**

```plain text
Input: nums = [6,4,3,2,7,6,2]
Output: [12,7,6]
Explanation:
- (6, 4) are non-coprime with LCM(6, 4) = 12. Now, nums = [12,3,2,7,6,2].
- (12, 3) are non-coprime with LCM(12, 3) = 12. Now, nums = [12,2,7,6,2].
- (12, 2) are non-coprime with LCM(12, 2) = 12. Now, nums = [12,7,6,2].
- (6, 2) are non-coprime with LCM(6, 2) = 6. Now, nums = [12,7,6].
There are no more adjacent non-coprime numbers in nums.
Thus, the final modified array is [12,7,6].
Note that there are other ways to obtain the same resultant array.
```

**Example 2:**

```plain text
Input: nums = [2,2,1,1,3,3,3]
Output: [2,1,1,3]
Explanation:
- (3, 3) are non-coprime with LCM(3, 3) = 3. Now, nums = [2,2,1,1,3,3].
- (3, 3) are non-coprime with LCM(3, 3) = 3. Now, nums = [2,2,1,1,3].
- (2, 2) are non-coprime with LCM(2, 2) = 2. Now, nums = [2,1,1,3].
There are no more adjacent non-coprime numbers in nums.
Thus, the final modified array is [2,1,1,3].
Note that there are other ways to obtain the same resultant array.
```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`
- The test cases are generated such that the values in the final array are **less than or equal** to `108`.
```java
class Solution {
    public List<Integer> replaceNonCoprimes(int[] nums) {
        Stack<Integer> stack = new Stack<>();
        
        for (int num : nums) {
            while (!stack.isEmpty()) {
                int top = stack.peek();
                int g = gcd(top, num);
                if (g == 1) {// 互斥
                    break;
                }
                stack.pop();
                num = (top / g) * num;  // 最大公因數
            }
            stack.push(num);
        }
        return stack;
    }
    
    private int gcd(int a, int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
}
```

