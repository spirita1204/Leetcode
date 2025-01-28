# 90. Subsets II

Methods: DFS
Difficulty: Medium

**Medium**

7.9K

226

Companies

Given an integer array `nums` that may contain duplicates, return *all possible*

*subsets*

*(the power set)*

.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]

```

**Constraints:**

- `1 <= nums.length <= 10`
- `10 <= nums[i] <= 10`

```java
class Solution {
    /**
        Each recursion level focuses on all the following elements. 
        We scan through all the following elements and decide whether to choose or not choose that element. 
        (Every level split into N branches.)
    */
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();

        helper(res, new ArrayList<>(), nums, 0);

        return res;
    }
    
    public void helper(List<List<Integer>> res, List<Integer> sub, int[] nums, int pos) {
        res.add(new ArrayList<>(sub));

        for(int i = pos; i < nums.length; i++) {
            if(i > pos && nums[i] == nums[i - 1]) continue;// **

            sub.add(nums[i]);

            helper(res, sub, nums, i + 1);     
a
            sub.remove(sub.size() - 1);
        }
    }
}
```