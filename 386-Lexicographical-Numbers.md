# 386. Lexicographical Numbers

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Given an integer `n`, return all the numbers in the range `[1, n]` sorted in lexicographical order.

You must write an algorithm that runs in `O(n)` time and uses `O(1)` extra space.

**Example 1:**

```
Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]

```

**Example 2:**

```
Input: n = 2
Output: [1,2]

```

**Constraints:**

- `1 <= n <= 5 * 104`

```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        //      1            2     3 ...
        // 1 10 11 12 13    2     3 ...
        // DFS
        List<Integer> res = new ArrayList<>();
        dfs(n, res, 1);

        return res;
    }
    private void dfs(int n, List<Integer> res, int init) {
        if(init > n) return;
     
        res.add(init);
        dfs(n, res, init * 10);
        if(init % 10 != 9)
            dfs(n, res, init + 1);
    }
}
```