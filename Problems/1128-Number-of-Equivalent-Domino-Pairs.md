# 1128. Number of Equivalent Domino Pairs  

  Methods: Combinatorics </br> Data Structure: Hash Table </br> Difficulty: Easy </br> </br>Given a list of `dominoes`, `dominoes[i] = [a, b]` is **equivalent to** `dominoes[j] = [c, d]` if and only if either (`a == c` and `b == d`), or (`a == d` and `b == c`) - that is, one domino can be rotated to be equal to another domino.

Return *the number of pairs *`(i, j)`* for which *`0 <= i < j < dominoes.length`*, and *`dominoes[i]`* is ****equivalent to**** *`dominoes[j]`.

**Example 1:**

```plain text
Input: dominoes = [[1,2],[2,1],[3,4],[5,6]]
Output: 1
```

**Example 2:**

```plain text
Input: dominoes = [[1,2],[1,2],[1,1],[1,2],[2,2]]
Output: 3
```

**Constraints:**

- `1 <= dominoes.length <= 4 * 104`
- `dominoes[i].length == 2`
- `1 <= dominoes[i][j] <= 9`
```java
class Solution {
        public int numEquivDominoPairs(int[][] dominoes) {
        Map<Integer, Integer> count = new HashMap<>();
        int res = 0;
        for (int[] d : dominoes) {
            int k = Math.min(d[0], d[1]) * 10 + Math.max(d[0], d[1]);
            count.put(k, count.getOrDefault(k, 0) + 1);
        }
        for (int v : count.values()) {
            res += v * (v - 1) / 2;
        }
        return res;
    }
}
```

