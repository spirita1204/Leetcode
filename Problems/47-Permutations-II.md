# 47. Permutations II

Methods: DFS
Difficulty: Medium

**Medium**

7.4K

129

Companies

Given a collection of numbers, `nums`, that might contain duplicates, return *all possible unique permutations **in any order**.*

**Example 1:**

```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]

```

**Example 2:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

```

**Constraints:**

- `1 <= nums.length <= 8`
- `10 <= nums[i] <= 10`

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        boolean[] used = new boolean[nums.length];
        dfs(new ArrayList<>(), res, nums, used);
        return res;
    }
    public void dfs(List<Integer> sub, List<List<Integer>> res, int[] nums, boolean[] used){
        if(sub.size() == nums.length){
            res.add(new ArrayList<Integer>(sub));
            return;
        }
        for(int i = 0; i< nums.length; i++){
            if(used[i]) continue;// 第i節點走過
            /**
            [1a, 1b, 2a], [1b, 1a, 2a]...,
            so we must make sure 1a goes before 1b to avoid duplicates
            By using nums[i-1]==nums[i] && !used[i-1], 
            we can make sure that 1b cannot be choosed before 
            */
            if(i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) continue;

            sub.add(nums[i]);
            used[i] = true;

            dfs(sub, res, nums, used);

            used[i] = false;
            sub.remove(sub.size() - 1);
        }
    }
}
```