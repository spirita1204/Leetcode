# 1444. Number of Ways of Cutting a Pizza

Data structure: Hash Table
Difficulty: Hard

**Hard**

763

44

```
class Solution {
    public int ways(String[] pizza, int k) {
        if(pizza == null || pizza.length == 0) return 0;
        Map<String, Long> memo = new HashMap<>();
        int tmp = (int)1e9 + 7;
        return (int)(dfs(pizza, memo, k, 0, pizza.length - 1, 0, pizza[0].length() - 1) % tmp);
    }
    
    private long dfs(String[] pizza, Map<String, Long> memo, int k, int rowS, int rowE, int colS, int colE) {
        if(rowS > rowE || colS > colE || k<=0) return 0;
        
        String key = rowS + ":" + rowE + ";" + colS + ":" + colE + ";" + k;
        if(memo.containsKey(key)) {
            return memo.get(key);
        }
        
        long res = 0;

        if(k == 1) {//切一等分
            res = isValid(pizza, rowS, rowE, colS, colE) ? 1 : 0;//有至少一顆回傳1 沒有回傳0
        }else{
            for(int i = rowS; i<=rowE; i++) {
                if(isValid(pizza, rowS, i, colS, colE)) {
                    res += dfs(pizza, memo, k - 1, i + 1, rowE, colS, colE);
                }
            }
            for(int i = colS; i<=colE; i++) {
                if(isValid(pizza, rowS, rowE, colS, i)) {
                    res += dfs(pizza, memo, k - 1, rowS, rowE, i + 1, colE);
                }
            }
        }
        
        memo.put(key, res);
        return res;
    }
    
    private boolean isValid(String[] pizza, int rowS, int rowE, int colS, int colE) {
        for(int i = rowS; i<=rowE; i++) {
            for(int j = colS; j<=colE; j++) {
                if(pizza[i].charAt(j) == 'A') return true;
            }
        }
        
        return false;
    }
}
```

For each cut you choose the direction: vertical or horizontal, then you choose a cut position at the cell boundary and cut the pizza into two pieces. If you cut the pizza vertically, give the left part of the pizza to a person. If you cut the pizza horizontally, give the upper part of the pizza to a person. Give the last piece of pizza to the last person.

*Return the number of ways of cutting the pizza such that each piece contains **at least** one apple.* Since the answer can be a huge number, return this modulo 10^9 + 7.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/04/23/ways_to_cut_apple_1.png](https://assets.leetcode.com/uploads/2020/04/23/ways_to_cut_apple_1.png)

```
Input: pizza = ["A..","AAA","..."], k = 3
Output: 3
Explanation: The figure above shows the three ways to cut the pizza. Note that pieces must contain at least one apple.

```

**Example 2:**

```
Input: pizza = ["A..","AA.","..."], k = 3
Output: 1

```

**Example 3:**

```
Input: pizza = ["A..","A..","..."], k = 1
Output: 1

```

**Constraints:**

- `1 <= rows, cols <= 50`
- `rows == pizza.length`
- `cols == pizza[i].length`
- `1 <= k <= 10`
- `pizza` consists of characters `'A'` and `'.'` only.