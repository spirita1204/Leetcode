# 14. Longest Common Prefix

Methods: Basic logic
Difficulty: Easy

Easy

Topics

Companies

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: strs = ["flower","flow","flight"]
Output: "fl"

```

**Example 2:**

```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.

```

**Constraints:**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        StringBuffer sb = new StringBuffer();
        Arrays.sort(strs);// 照字母排序

        if (strs.length != 0) {
            char[] first = strs[0].toCharArray();
            char[] last = strs[strs.length - 1].toCharArray();// 直接第一個和最後一個 比較即可
            for (int i = 0; i < first.length; i++) {
                if (first[i] == last[i]) {
                    sb.append(first[i]);
                } else {
                    return sb.toString();
                }
            }
        }
        return sb.toString();
    }
}
```