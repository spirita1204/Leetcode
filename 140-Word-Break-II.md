# 140. Word Break II

Methods: DFS
Difficulty: Hard

Hard

Topics

Companies

Given a string `s` and a dictionary of strings `wordDict`, add spaces in `s` to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in **any order**.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

```
Input: s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
Output: ["cats and dog","cat sand dog"]

```

**Example 2:**

```
Input: s = "pineapplepenapple", wordDict = ["apple","pen","applepen","pine","pineapple"]
Output: ["pine apple pen apple","pineapple pen apple","pine applepen apple"]
Explanation: Note that you are allowed to reuse a dictionary word.

```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: []

```

**Constraints:**

- `1 <= s.length <= 20`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 10`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of `wordDict` are **unique**.
- Input is generated in a way that the length of the answer doesn't exceed 10.
    
    5
    
    ```java
    class Solution {
        public List<String> wordBreak(String s, List<String> wordDict) {
            List<String> res = new ArrayList<>();
            backtracking(s, wordDict, 0, res, new StringBuilder());
    
            return res;
        }
    
        private void backtracking (String s, List<String> wordDict, int i, List<String> res, StringBuilder sb) {
            if(i == s.length()) {
                res.add(sb.toString().substring(0, sb.length() - 1));// 去掉最後空白
            }
            for(int j = i; j <= s.length(); j++) {
                String sub = s.substring(i, j);
                if(wordDict.contains(sub)) {
                    sb.append(sub).append(" ");
                    backtracking(s, wordDict, j, res, sb);
                    sb.delete(sb.length() - sub.length() - 1, sb.length());
                }else {
                    continue;
                }     
    
            }
        }
    }
    ```