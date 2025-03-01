# 1092. Shortest Common Supersequence   

  Methods: DP </br> Difficulty: Hard </br> </br>Given two strings `str1` and `str2`, return *the shortest string that has both *`str1`* and *`str2`* as ****subsequences***. If there are multiple valid strings, return **any** of them.

A string `s` is a **subsequence** of string `t` if deleting some number of characters from `t` (possibly `0`) results in the string `s`.

**Example 1:**

```plain text
Input: str1 = "abac", str2 = "cab"
Output: "cabac"
Explanation:
str1 = "abac" is a subsequence of "cabac" because we can delete the first "c".
str2 = "cab" is a subsequence of "cabac" because we can delete the last "ac".
The answer provided is the shortest such string that satisfies these properties.

```

**Example 2:**

```plain text
Input: str1 = "aaaaaaaa", str2 = "aaaaaaaa"
Output: "aaaaaaaa"

```

**Constraints:**

- `1 <= str1.length, str2.length <= 1000`
- `str1` and `str2` consist of lowercase English letters.
---

Hint 1

We can find the length of the longest common subsequence between str1[i:] and str2[j:] (for all (i, j)) by using dynamic programming.

---

Hint 2

We can use this information to recover the shortest common supersequence.

### 1.

### 2.喪心病狂作法

```java
class Solution {
    public String shortestCommonSupersequence(String str1, String str2) {
        String res = "";
        try {
            Callable<String> task = () -> generateLCS(str1, str2);
            FutureTask<String> future = new FutureTask<>(task);
            new Thread(future).start();
            res = future.get();
        } catch (Exception e) {

        }
        return res;
    }

    public String generateLCS(String str1, String str2) {

        int m = str1.length();
        int n = str2.length();
        int[][] lcsMatrix = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (str1.charAt(i - 1) == str2.charAt(j - 1)) {
                    lcsMatrix[i][j] = lcsMatrix[i - 1][j - 1] + 1;
                } else {
                    lcsMatrix[i][j] = Math.max(lcsMatrix[i - 1][j], lcsMatrix[i][j - 1]);
                }
            }
        }
        int row = m, col = n;
        StringBuilder ans = new StringBuilder();
        while (row > 0 && col > 0) {
            if (str1.charAt(row - 1) == str2.charAt(col - 1)) {
                ans.append(str1.charAt(row - 1));
                row--;
                col--;
            } else if (lcsMatrix[row - 1][col] > lcsMatrix[row][col - 1]) {
                ans.append(str1.charAt(row - 1));
                row--;
            } else {
                ans.append(str2.charAt(col - 1));
                col--;
            }
        }
        while (row > 0) {
            ans.append(str1.charAt(row - 1));
            row--;
        }
        while (col > 0) {
            ans.append(str2.charAt(col - 1));
            col--;
        }
        return ans.reverse().toString();
    }
}

```

