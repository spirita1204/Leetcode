# 399. Evaluate Division

Methods: DFS
Data structure: Set
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]` represent the equation `Ai / Bi = values[i]`. Each `Ai` or `Bi` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [Cj, Dj]` represents the `jth` query where you must find the answer for `Cj / Dj = ?`.

Return *the answers to all queries*. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Note:** The variables that do not occur in the list of equations are undefined, so the answer cannot be determined for them.

**Example 1:**

```
Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation:
Given:a / b = 2.0,b / c = 3.0
queries are:a / c = ?,b / a = ?,a / e = ?,a / a = ?,x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
note: x is undefined => -1.0
```

**Example 2:**

```
Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
Output: [3.75000,0.40000,5.00000,0.20000]

```

**Example 3:**

```
Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
Output: [0.50000,2.00000,-1.00000,-1.00000]

```

**Constraints:**

- `1 <= equations.length <= 20`
- `equations[i].length == 2`
- `1 <= Ai.length, Bi.length <= 5`
- `values.length == equations.length`
- `0.0 < values[i] <= 20.0`
- `1 <= queries.length <= 20`
- `queries[i].length == 2`
- `1 <= Cj.length, Dj.length <= 5`
- `Ai, Bi, Cj, Dj` consist of lower case English letters and digits.

```java
class Solution {
    class Node {
        String num;
        double val;

        Node(String num, double val) {
            this.num = num;
            this.val = val;
        }
    }

    // 轉成以下結構
    // a : [b, 2.0], [c, 3.0];
    // b : [a, 0.5], ...
    Map<String, List<Node>> map = new HashMap<>();

    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        double[] res = new double[queries.size()];

        for (int i = 0; i < equations.size(); i++) {
            List<String> equation = equations.get(i);
            String fir = equation.get(0);
            String sec = equation.get(1);
            if (!map.containsKey(fir)) {// a/ b存放
                map.put(fir, new ArrayList<>());
            }
            map.get(fir).add(new Node(sec, values[i]));
            if (!map.containsKey(sec)) {// b/ a存放
                map.put(sec, new ArrayList<>());
            }
            map.get(sec).add(new Node(fir, 1 / values[i]));
        }

        for(int i = 0; i< res.length; i++) {
            String fir = queries.get(i).get(0);
            String sec = queries.get(i).get(1);

            res[i] = dfs(fir, sec, 1, new HashSet<>());
        }
        return res;
    }
    private double dfs (String fir, String sec, double value, HashSet<String> visited) {// visited防止重複找
        if(!map.containsKey(fir)) return -1;
        //
        if(visited.contains(fir)) return -1;

        if(fir.equals(sec)) return value;
        // 避免重複遍歷
        visited.add(fir);
        // (a/b ) * (b/ c)...
        for(Node next: map.get(fir)) {
            double sub = dfs(next.num, sec, value * next.val, visited);
            if(sub != -1.0) return sub;
        }
        visited.remove(fir);

        return -1;
    }
}

```