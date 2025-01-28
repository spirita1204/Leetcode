# 77. Combinations

Methods: DFS
Difficulty: Medium

Given two integers `n` and `k`, return *all possible combinations of* `k` *numbers chosen from the range* `[1, n]`.

You may return the answer in **any order**.

**Example 1:**

```
Input: n = 4, k = 2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Explanation: There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.

```

**Example 2:**

```
Input: n = 1, k = 1
Output: [[1]]
Explanation: There is 1 choose 1 = 1 total combination.

```

**Constraints:**

- `1 <= n <= 20`
- `1 <= k <= n`

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> list = new ArrayList<>();
        dfs(n, k, 1, 0, list, new ArrayList<>());
        return list;
    }
    public void dfs(int n, int level, int now, int nowLevel, List<List<Integer>> list, List<Integer> sublist){
        //數字,限制走到幾層,數字不重複,now到第幾個數字不重複,list,sublist
        if(nowLevel >= level){
            list.add(new ArrayList<>(sublist));
            return;
        }
        for(int i = now; i <= n; i++){
            sublist.add(now);
            now++;
            dfs(n, level, now, nowLevel + 1, list, sublist);
            sublist.remove(sublist.size() - 1);
        }
    }
}
```