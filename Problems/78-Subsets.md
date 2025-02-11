# 78. Subsets

Methods: DFS
Difficulty: Medium

**Medium**

14.2K

204

Companies

Given an integer array `nums` of **unique** elements, return *all possible*

*subsets*

*(the power set)*

.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]

```

**Constraints:**

- `1 <= nums.length <= 10`
- `10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if(nums.length == 0 || nums == null ) return res;

        dfs(nums, 0, res, new ArrayList<>());

        return res;
    }
    public void dfs(int[] nums,int i, List<List<Integer>> res, List<Integer> sub){
        if(i == nums.length){ 
            res.add(new ArrayList<>(sub));
            return;
        }
        sub.add(nums[i]);
        dfs(nums, i + 1, res, sub);
        sub.remove(sub.size() - 1);
        dfs(nums, i + 1, res, sub);
    }
}
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if(nums.length == 0 || nums == null ) return res;

        dfs(nums, 0, res, new ArrayList<>());

        return res;
    }
    public void dfs(int[] nums,int idx, List<List<Integer>> res, List<Integer> sub){
        res.add(new ArrayList<>(sub));
        if(idx == nums.length) {
            return;
        }
        for(int i = idx; i< nums.length; i++) {
            sub.add(nums[i]);
            dfs(nums, i + 1, res, sub);
            sub.remove(sub.size() - 1);
        }
    }
}
```