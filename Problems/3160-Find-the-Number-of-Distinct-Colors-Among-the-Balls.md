# 3160. Find the Number of Distinct Colors Among the Balls  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given an integer `limit` and a 2D array `queries` of size `n x 2`.

There are `limit + 1` balls with **distinct** labels in the range `[0, limit]`. Initially, all balls are uncolored. For every query in `queries` that is of the form `[x, y]`, you mark ball `x` with the color `y`. After each query, you need to find the number of **distinct** colors among the balls.

Return an array `result` of length `n`, where `result[i]` denotes the number of distinct colors *after* `ith` query.

**Note** that when answering a query, lack of a color *will not* be considered as a color.

**Example 1:**

**Input:** limit = 4, queries = [[1,4],[2,5],[1,3],[3,4]]

**Output:** [1,2,2,3]

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/04/17/ezgifcom-crop.gif)

- After query 0, ball 1 has color 4.
- After query 1, ball 1 has color 4, and ball 2 has color 5.
- After query 2, ball 1 has color 3, and ball 2 has color 5.
- After query 3, ball 1 has color 3, ball 2 has color 5, and ball 3 has color 4.
**Example 2:**

**Input:** limit = 4, queries = [[0,1],[1,2],[2,2],[3,4],[4,5]]

**Output:** [1,2,2,3,4]

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2024/04/17/ezgifcom-crop2.gif)

- After query 0, ball 0 has color 1.
- After query 1, ball 0 has color 1, and ball 1 has color 2.
- After query 2, ball 0 has color 1, and balls 1 and 2 have color 2.
- After query 3, ball 0 has color 1, balls 1 and 2 have color 2, and ball 3 has color 4.
- After query 4, ball 0 has color 1, balls 1 and 2 have color 2, ball 3 has color 4, and ball 4 has color 5.
**Constraints:**

- `1 <= limit <= 109`
- `1 <= n == queries.length <= 105`
- `queries[i].length == 2`
- `0 <= queries[i][0] <= limit`
- `1 <= queries[i][1] <= 109`
```java
class Solution {
    public int[] queryResults(int limit, int[][] queries) {
        int len = queries.length;
        int[] res = new int[len];
        Map<Integer, Integer> elements = new HashMap<>();
        Map<Integer, Integer> hm = new HashMap<>();// color, cnt;

        for (int i = 0; i < len; i++) {
            int pos = queries[i][0];
            int color = queries[i][1];
             if (!elements.containsKey(pos)) {
                elements.put(pos, color);// 給定指定位子顏色
                hm.put(color, hm.getOrDefault(color, 0) + 1);
            } else {// 已經有顏色
                int preColor = elements.get(pos);  // 位置的原有顏色
                if (preColor != color) {
                    // 移除原有顏色的cnt
                    int preCount = hm.get(preColor) - 1;
                    hm.put(preColor, preCount);  // 更新原有顏色的cnt
                    if (preCount == 0) {
                        hm.remove(preColor);  // 顏色cnt = 0
                    }
                    // 新顏色的cnt
                    hm.put(color, hm.getOrDefault(color, 0) + 1);
                    // 更新位置的顏色
                    elements.put(pos, color);
                }
            }
            res[i] = hm.size();
        }
        return res;
    }
}
```

