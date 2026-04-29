# 2615. Sum of Distances  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given a **0-indexed** integer array `nums`. There exists an array `arr` of length `nums.length`, where `arr[i]` is the sum of `|i - j|` over all `j` such that `nums[j] == nums[i]` and `j != i`. If there is no such `j`, set `arr[i]` to be `0`.

Return *the array *`arr`*.*

**Example 1:**

```plain text
Input: nums = [1,3,1,1,2]
Output: [5,0,3,4,0]
Explanation:
When i = 0, nums[0] == nums[2] and nums[0] == nums[3]. Therefore, arr[0] = |0 - 2| + |0 - 3| = 5.
When i = 1, arr[1] = 0 because there is no other index with value 3.
When i = 2, nums[2] == nums[0] and nums[2] == nums[3]. Therefore, arr[2] = |2 - 0| + |2 - 3| = 3.
When i = 3, nums[3] == nums[0] and nums[3] == nums[2]. Therefore, arr[3] = |3 - 0| + |3 - 2| = 4.
When i = 4, arr[4] = 0 because there is no other index with value 2.
```

**Example 2:  **

```plain text
Input: nums = [0,5,3]
Output: [0,0,0]
Explanation: Since each element in nums is distinct, arr[i] = 0 for all i.   
```

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`
**Note:** This question is the same as [2121: Intervals Between Identical Elements.](https://leetcode.com/problems/intervals-between-identical-elements/description/)

```java
class Solution {
    public long[] distance(int[] nums) {
        int n = nums.length;
        long[] ans = new long[n];

        Map<Integer, List<Integer>> mp = new HashMap<>();

        for (int i = 0; i < n; i++) {
            mp.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
        }

        for (List<Integer> pos : mp.values()) {

            long sum = 0;
            for (int x : pos) 
                sum += x;

            long leftSum = 0;
            int m = pos.size();

            for (int i = 0; i < m; i++) {
                long rightSum = sum - leftSum - pos.get(i);
                // (pos[i] - pos[0]) + (pos[i] - pos[1]) + ...
                // -> 等同 pos[i] * i - 左邊總和
                long left  = (long) pos.get(i) * i - leftSum;
                // (pos[i+1] - pos[i]) + (pos[i+2] - pos[i]) + ...
                // -> 等同 右邊總和 - pos[i] * (右邊個數)
                long right = rightSum - (long) pos.get(i) * (m - i - 1);
                // 距離拆成 : 左邊 + 右邊
                ans[pos.get(i)] = left + right;

                leftSum += pos.get(i);
            }
        }

        return ans;
    }
}
```

