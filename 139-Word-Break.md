# 139. Word Break

Methods: DFS
Difficulty: Medium

**Medium**

13.9K

587

Companies

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".

```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false

```

**Constraints:**

- `1 <= s.length <= 300`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 20`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of `wordDict` are **unique**.

TLE 用遞迴解

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return dfs(s, wordDict);
    }

    public boolean dfs(String s, List<String> wordDict) {// 
        if(wordDict.contains(s)) return true;

        for(int i = 1; i< s.length(); i++){
            boolean left = dfs(s.substring(0, i), wordDict);
            boolean right = dfs(s.substring(i), wordDict);
          
            if(left && right) return true;
        }
        return false;
    }
}
```

Recursion + Memo

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {// memo + recursion記憶化遞歸
        return dfs(s, wordDict, 0, new Boolean[s.length()]);
    }

    public boolean dfs(String s, List<String> wordDict, int start, Boolean[] memo) {// check用來避免重複計算
        if(start == s.length()) return true;
        // 當該字串已有解 不用繼續遞歸往下找
        if(memo[start] != null) return memo[start];

        for(int end = start+ 1; end<= s.length(); end++){
            // 左邊substr% 右邊substr成立
            if(wordDict.contains(s.substring(start, end)) && dfs(s, wordDict, end, memo)){
                // 將遞迴結果存入memo 再回傳
                return memo[start] = true;
            }
        }
        return memo[start] = false;
    }
}
```