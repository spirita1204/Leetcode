# 2221. Find Triangular Sum of an Array  

  Methods: Array </br> Difficulty: Medium </br> </br>You are given a **0-indexed** integer array `nums`, where `nums[i]` is a digit between `0` and `9` (**inclusive**).

The **triangular sum** of `nums` is the value of the only element present in `nums` after the following process terminates:

1. Let `nums` comprise of `n` elements. If `n == 1`, **end** the process. Otherwise, **create** a new **0-indexed** integer array `newNums` of length `n - 1`.
1. For each index `i`, where `0 <= i < n - 1`, **assign** the value of `newNums[i]` as `(nums[i] + nums[i+1]) % 10`, where `%` denotes modulo operator.
1. **Replace** the array `nums` with `newNums`.
1. **Repeat** the entire process starting from step 1.
Return *the triangular sum of* `nums`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2022/02/22/ex1drawio.png)

```plain text
Input: nums = [1,2,3,4,5]
Output: 8
Explanation:
The above diagram depicts the process from which we obtain the triangular sum of the array.
```

**Example 2:**

```plain text
Input: nums = [5]
Output: 5
Explanation:
Since there is only one element in nums, the triangular sum is the value of that element itself.
```

**Constraints:**

- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 9`
```java
class Solution {
    public int triangularSum(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for (int num : nums) list.add(num);

        while (list.size() != 1) {
            List<Integer> temp = new ArrayList<>();
            for (int i = 0; i < list.size() - 1; i++) {
                int val = (list.get(i) + list.get(i + 1)) % 10;
                temp.add(val);
            }
            list = temp;
        }
        return list.get(0);
    }
}
```

