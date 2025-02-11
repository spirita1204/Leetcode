# 46. Permutations

Methods: DFS
Difficulty: Medium

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

```

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]

```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(new ArrayList<>(),res,nums);
        return res;
    }
    public void dfs(List<Integer> sub, List<List<Integer>> res, int[] nums){
        if(sub.size() == nums.length){
            res.add(new ArrayList<Integer>(sub));
            return;
        }
        for(int i : nums){
            if(sub.contains(i))continue;
            sub.add(i);
            dfs(sub,res,nums);
            sub.remove(sub.size() - 1);
        }
    }
}
```