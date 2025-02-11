# 2216. Minimum Deletions to Make Array Beautiful

Methods: Greedy
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a **0-indexed** integer array `nums`. The array `nums` is **beautiful** if:

- `nums.length` is even.
- `nums[i] != nums[i + 1]` for all `i % 2 == 0`.

Note that an empty array is considered beautiful.

You can delete any number of elements from `nums`. When you delete an element, all the elements to the right of the deleted element will be **shifted one unit to the left** to fill the gap created and all the elements to the left of the deleted element will remain **unchanged**.

Return *the **minimum** number of elements to delete from* `nums` *to make it beautiful.*

**Example 1:**

```
Input: nums = [1,1,2,3,5]
Output: 1
Explanation: You can delete eithernums[0] ornums[1] to makenums = [1,2,3,5] which is beautiful. It can be proven you need at least 1 deletion to makenums beautiful.

```

**Example 2:**

```
Input: nums = [1,1,2,2,3,3]
Output: 2
Explanation: You can deletenums[0] andnums[5] to make nums = [1,2,2,3] which is beautiful. It can be proven you need at least 2 deletions to make nums beautiful.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`

```java
class Solution {
    public int minDeletion(int[] nums) {
        // greedy 由左至右 兩兩掃遇到不成立就刪除
        int res = 0;
        int len = nums.length;
        int p2 = 0;// 指標往後找下位
        while(p2 + 1 < len) {
            int fir = nums[p2];
            int sec = nums[p2 + 1];
            if(fir != sec) 
                p2 += 2;
            else {// 刪掉其中一個
                res++;
                p2++;// 刪掉一個往前走一位停
            }
        }
        if(p2 == len - 1) res++;
        return res;
    }
}
```