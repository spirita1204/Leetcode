# 2976. Minimum Cost to Convert String I

Methods: DP, Shortest Path
Data structure: Graph
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given two **0-indexed** strings `source` and `target`, both of length `n` and consisting of **lowercase** English letters. You are also given two **0-indexed** character arrays `original` and `changed`, and an integer array `cost`, where `cost[i]` represents the cost of changing the character `original[i]` to the character `changed[i]`.

You start with the string `source`. In one operation, you can pick a character `x` from the string and change it to the character `y` at a cost of `z` **if** there exists **any** index `j` such that `cost[j] == z`, `original[j] == x`, and `changed[j] == y`.

Return *the **minimum** cost to convert the string* `source` *to the string* `target` *using **any** number of operations. If it is impossible to convert* `source` *to* `target`, *return* `-1`.

**Note** that there may exist indices `i`, `j` such that `original[j] == original[i]` and `changed[j] == changed[i]`.

**Example 1:**

```
Input: source = "abcd", target = "acbe", original = ["a","b","c","c","e","d"], changed = ["b","c","b","e","b","e"], cost = [2,5,5,1,2,20]
Output: 28
Explanation: To convert the string "abcd" to string "acbe":
- Change value at index 1 from 'b' to 'c' at a cost of 5.
- Change value at index 2 from 'c' to 'e' at a cost of 1.
- Change value at index 2 from 'e' to 'b' at a cost of 2.
- Change value at index 3 from 'd' to 'e' at a cost of 20.
The total cost incurred is 5 + 1 + 2 + 20 = 28.
It can be shown that this is the minimum possible cost.

```

**Example 2:**

```
Input: source = "aaaa", target = "bbbb", original = ["a","c"], changed = ["c","b"], cost = [1,2]
Output: 12
Explanation: To change the character 'a' to 'b' change the character 'a' to 'c' at a cost of 1, followed by changing the character 'c' to 'b' at a cost of 2, for a total cost of 1 + 2 = 3. To change all occurrences of 'a' to 'b', a total cost of 3 * 4 = 12 is incurred.

```

**Example 3:**

```
Input: source = "abcd", target = "abce", original = ["a"], changed = ["e"], cost = [10000]
Output: -1
Explanation: It is impossible to convert source to target because the value at index 3 cannot be changed from 'd' to 'e'.

```

**Constraints:**

- `1 <= source.length == target.length <= 105`
- `source`, `target` consist of lowercase English letters.
- `1 <= cost.length == original.length == changed.length <= 2000`
- `original[i]`, `changed[i]` are lowercase English letters.
- `1 <= cost[i] <= 106`
- `original[i] != changed[i]`

```java
class Solution {
    public long minimumCost(String source, String target, char[] original, char[] changed, int[] cost) {
        long[][] dis = new long[26][26];
        // 距離100000 + 1代表到不了
        for (long[] row : dis)
            Arrays.fill(row, 100000* (26-1) + 1);
        for(int i = 0; i< original.length; i++){// 單向
            char c1 = original[i];
            char c2 = changed[i];
            dis[c1 - 'a'][c2 - 'a'] = Math.min(dis[c1 - 'a'][c2 - 'a'], cost[i]);
        }
        // 建立最短路徑
        for(int r = 0; r < 26; r++)
            for(int i = 0; i < 26; i++)
                for(int j = 0; j < 26; j++)
                    dis[i][j] = Math.min(dis[i][j], dis[i][r] + dis[r][j]);
        // 遍歷
        long res = 0;
        for(int i = 0; i < source.length(); i++) {
            char c1 = source.charAt(i);
            char c2 = target.charAt(i);
            long e = dis[c1 - 'a'][c2 - 'a'];
            if(e == 100000* (26-1) + 1 && c1 != c2) return -1;
            if(c1 != c2) res += e;
        }
        return res;
    }
}
```