# 3354. Make Array Elements Equal to Zero  

  Methods: Prefix Sum </br> Difficulty: Easy,Medium </br> </br>You are given an integer array `nums`.  

Start by selecting a starting position `curr` such that `nums[curr] == 0`, and choose a movement **direction** of either left or right.

After that, you repeat the following process:

- If `curr` is out of the range `[0, n - 1]`, this process ends.
- If `nums[curr] == 0`, move in the current direction by **incrementing** `curr` if you are moving right, or **decrementing** `curr` if you are moving left.
- Else if `nums[curr] > 0`:
A selection of the initial position `curr` and movement direction is considered **valid** if every element in `nums` becomes 0 by the end of the process.

Return the number of possible **valid** selections.

**Example 1:**

**Input:** nums = [1,0,2,0,3]

**Output:** 2

**Explanation:**

The only possible valid selections are the following:

- Choose `curr = 3`, and a movement direction to the left.
- Choose `curr = 3`, and a movement direction to the right.
**Example 2:**

**Input:** nums = [2,3,4,0,4,1,0]

**Output:** 0

**Explanation:**

There are no possible valid selections.

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 100`
- There is at least one element `i` where `nums[i] == 0`.
```java
class Solution {
    public int countValidSelections(int[] nums) {
        int n = nums.length;
        int[] prefixSum = new int[n + 1];
        // 從某個位置開始，若左邊的總和等於右邊的總和，就可以左右都走，否則只能走一邊（如果差值是 1）。
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }

        int res = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] == 0) {
                if (prefixSum[n] == 2 * prefixSum[i]) {
                    res += 2;// 左右方向都可以
                } else if (Math.abs(prefixSum[n] - 2 * prefixSum[i]) == 1) {
                    res += 1;// 只有一個方向可以
                }
            }
        }

        return res;
    }
}
```

