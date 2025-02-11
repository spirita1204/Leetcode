# 3152. Special Array II

Methods: Prefix Sum
Difficulty: Medium

Medium

Topics

Companies

Hint

An array is considered **special** if every pair of its adjacent elements contains two numbers with different parity.

You are given an array of integer `nums` and a 2D integer matrix `queries`, where for `queries[i] = [fromi, toi]` your task is to check that

subarray

```
nums[fromi..toi]
```

is

**special**

or not.

Return an array of booleans `answer` such that `answer[i]` is `true` if `nums[fromi..toi]` is special.

**Example 1:**

**Input:** nums = [3,4,1,2,6], queries = [[0,4]]

**Output:** [false]

**Explanation:**

The subarray is `[3,4,1,2,6]`. 2 and 6 are both even.

**Example 2:**

**Input:** nums = [4,3,1,6], queries = [[0,2],[2,3]]

**Output:** [false,true]

**Explanation:**

1. The subarray is `[4,3,1]`. 3 and 1 are both odd. So the answer to this query is `false`.
2. The subarray is `[1,6]`. There is only one pair: `(1,6)` and it contains numbers with different parity. So the answer to this query is `true`.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`
- `1 <= queries.length <= 105`
- `queries[i].length == 2`
- `0 <= queries[i][0] <= queries[i][1] <= nums.length - 1`

```java
class Solution {
    public boolean[] isArraySpecial(int[] nums, int[][] queries) {
        boolean[] res = new boolean[queries.length];
        int[] ps = new int[nums.length];
        for (int i = 1; i < nums.length; i++) {
            ps[i] = ps[i - 1];
            if (nums[i - 1] % 2 == nums[i] % 2) {// 當相同作記號
                ps[i]++;
            }
        }
        for (int i = 0; i < queries.length; i++) {
            int from = queries[i][0];
            int to = queries[i][1];
            int cnt = ps[to] - ps[from];
            res[i] = cnt > 0 ? false : true;
        }
        return res;
    }
}
```