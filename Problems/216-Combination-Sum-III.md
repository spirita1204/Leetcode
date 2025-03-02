# 216. Combination Sum III

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers `1` through `9` are used.
- Each number is used **at most once**.

Return *a list of all possible valid combinations*. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1:**

```
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

**Example 2:**

```
Input: k = 3, n = 9
Output: [[1,2,6],[1,3,5],[2,3,4]]
Explanation:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.

```

**Example 3:**

```
Input: k = 4, n = 1
Output: []
Explanation: There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.

```

**Constraints:**

- `2 <= k <= 9`
- `1 <= n <= 60`

```java
class Solution {
    int[] arr = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(0, n, new ArrayList<>(), k);
        return res;
    }
    private void dfs(int now, int sum, List<Integer> sub, int k) {
        for(int i = now; i < arr.length; i++) {
            if(sum - arr[i] > 0) {
                sub.add(arr[i]);
                dfs(i + 1, sum - arr[i], sub, k - 1);
                sub.remove(sub.size() - 1);
            } else if(sum == arr[i] && k == 1) {
                sub.add(arr[i]);
                res.add(new ArrayList<>(sub));
                sub.remove(sub.size() - 1);
                return;
            } else {
                return;
            }
        }
    }
}
```