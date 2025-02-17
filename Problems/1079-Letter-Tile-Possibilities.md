# 1079. Letter Tile Possibilities  

  Methods: DFS </br> Difficulty: Medium </br> </br>You have `n`  `tiles`, where each tile has one letter `tiles[i]` printed on it.

Return *the number of possible non-empty sequences of letters* you can make using the letters printed on those `tiles`.

**Example 1: **

```plain text
Input: tiles = "AAB"
Output: 8
Explanation:The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".

```

**Example 2:**

```plain text
Input: tiles = "AAABBC"
Output: 188

```

**Example 3:**

```plain text
Input: tiles = "V"
Output: 1

```

**Constraints:**

- `1 <= tiles.length <= 7`
- `tiles` consists of uppercase English letters.
```java
class Solution {
    public int numTilePossibilities(String tiles) {
        int freq[] = new int[26];
        for (char c : tiles.toCharArray())
            freq[c - 'A']++;  // 計算每個字母的頻率
        return dfs(freq);  
    }

    private int dfs(int freq[]) {
        int count = 0;
        for (int i = 0; i < freq.length; i++) {
            if (freq[i] > 0) {  // 如果該字母還有剩餘
                freq[i]--;  // 選擇這個字母
                count += dfs(freq) + 1;  // 計算選擇這個字母後的所有組合，並加 1 計算當前字母的組合
                freq[i]++;  // 恢復字母的頻率
            }
        }
        return count;
    }
}

```

