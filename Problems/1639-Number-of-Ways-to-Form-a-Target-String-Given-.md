# 1639. Number of Ways to Form a Target String Given a Dictionary

Methods: DP
Difficulty: Hard

**Hard**

1K

55

Companies

You are given a list of strings of the **same length** `words` and a string `target`.

Your task is to form `target` using the given `words` under the following rules:

- `target` should be formed from left to right.
- To form the `ith` character (**0-indexed**) of `target`, you can choose the `kth` character of the `jth` string in `words` if `target[i] = words[j][k]`.
- Once you use the `kth` character of the `jth` string of `words`, you **can no longer** use the `xth` character of any string in `words` where `x <= k`. In other words, all characters to the left of or at index `k` become unusuable for every string.
- Repeat the process until you form the string `target`.

**Notice** that you can use **multiple characters** from the **same string** in `words` provided the conditions above are met.

Return *the number of ways to form `target` from `words`*. Since the answer may be too large, return it **modulo** `109 + 7`.

**Example 1:**

```
Input: words = ["acca","bbbb","caca"], target = "aba"
Output: 6
Explanation: There are 6 ways to form target.
"aba" -> index 0 ("acca"), index 1 ("bbbb"), index 3 ("caca")
"aba" -> index 0 ("acca"), index 2 ("bbbb"), index 3 ("caca")
"aba" -> index 0 ("acca"), index 1 ("bbbb"), index 3 ("acca")
"aba" -> index 0 ("acca"), index 2 ("bbbb"), index 3 ("acca")
"aba" -> index 1 ("caca"), index 2 ("bbbb"), index 3 ("acca")
"aba" -> index 1 ("caca"), index 2 ("bbbb"), index 3 ("caca")

```

**Example 2:**

```
Input: words = ["abba","baab"], target = "bab"
Output: 4
Explanation: There are 4 ways to form target.
"bab" -> index 0 ("baab"), index 1 ("baab"), index 2 ("abba")
"bab" -> index 0 ("baab"), index 1 ("baab"), index 3 ("baab")
"bab" -> index 0 ("baab"), index 2 ("baab"), index 3 ("baab")
"bab" -> index 1 ("abba"), index 2 ("baab"), index 3 ("baab")

```

**Constraints:**

- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 1000`
- All strings in `words` have the same length.
- `1 <= target.length <= 1000`
- `words[i]` and `target` contain only lowercase English letters.

![Untitled](Untitled%2017.png)

```jsx
class Solution {
    public int numWays(String[] words, String target) {
        int[][] count =  new int[26][ words[0].length()];
        int mod = (int)1e9 + 7;

        for(int i= 0; i< words[0].length(); i++){// 各index字母頻率
            for(int j= 0; j< words.length; j++){
                count[ words[j].charAt(i)- 'a' ][i]++;
            }
        }
        // 用word第i元素前去組成target到第j的元素
        long dp[][] = new long[target.length()+1][words[0].length()+1];

        for(int i= 0; i< dp[0].length; i++) dp[0][i] = 1;// 用word[0:i]去構建target="" 都不取=1

        for(int i = 1; i<= target.length(); i++){
            for(int j = 1; j<= words[0].length(); j++){
                //不使用word[j]去建構target[i] ; target[i] = word[j-1]
                dp[i][j] = dp[i][j-1];  
                //使用word[j]去建構target[i] ; 乘上他有幾個選擇
                if(count[target.charAt(i-1)- 'a'][j-1] > 0){// 減1對應count
                    dp[i][j] += (dp[i-1][j-1]* count[target.charAt(i-1)- 'a'][j-1]) % mod;
                }
                dp[i][j] %= mod;
            }
        }
        return (int)dp[target.length()][words[0].length()];
    }
}
```