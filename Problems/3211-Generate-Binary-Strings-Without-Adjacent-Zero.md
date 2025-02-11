# 3211. Generate Binary Strings Without Adjacent Zeros

Methods: DFS
Difficulty: Medium

Solved

Medium

Companies

Hint

You are given a positive integer `n`.

A binary string `x` is **valid** if all

substrings

of

```
x
```

of length 2 contain

**at least**

one

```
"1"
```

.

Return all **valid** strings with length `n`**,** in *any* order.

**Example 1:**

**Input:** n = 3

**Output:** ["010","011","101","110","111"]

**Explanation:**

The valid strings of length 3 are: `"010"`, `"011"`, `"101"`, `"110"`, and `"111"`.

**Example 2:**

**Input:** n = 1

**Output:** ["0","1"]

**Explanation:**

The valid strings of length 1 are: `"0"` and `"1"`.

**Constraints:**

- `1 <= n <= 18`

```java
class Solution {
    List<String> res = new ArrayList<>();
    
    public List<String> validStrings(int n) {
        StringBuilder sb = new StringBuilder();
        dfs(sb, n);
        
        return res;
    }
    private void dfs(StringBuilder sb, int n) {
        if(sb.length() == n) {
            res.add(sb.toString());
            return;
        }    
            if(sb.length() == 0) {
                sb.append('0');
                dfs(sb, n);
                sb.deleteCharAt(sb.length() - 1);
                sb.append('1');
                dfs(sb, n);
                sb.deleteCharAt(sb.length() - 1);
            } else {
                if(sb.charAt(sb.length() - 1) == '0') {
                    sb.append('1');
                    dfs(sb, n);
                    sb.deleteCharAt(sb.length() - 1);
                } else {
                    sb.append('0');
                    dfs(sb, n);
                    sb.deleteCharAt(sb.length() - 1);
                    sb.append('1');
                    dfs(sb, n);  
                    sb.deleteCharAt(sb.length() - 1);
                }
            }
    }    
}
```