# 1239. Maximum Length of a Concatenated String with Unique Characters

Methods: DFS
Data structure: Set
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given an array of strings `arr`. A string `s` is formed by the **concatenation** of a **subsequence** of `arr` that has **unique characters**.

Return *the **maximum** possible length* of `s`.

A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

**Example 1:**

```
Input: arr = ["un","iq","ue"]
Output: 4
Explanation: All the valid concatenations are:
- ""
- "un"
- "iq"
- "ue"
- "uniq" ("un" + "iq")
- "ique" ("iq" + "ue")
Maximum length is 4.

```

**Example 2:**

```
Input: arr = ["cha","r","act","ers"]
Output: 6
Explanation: Possible longest valid concatenations are "chaers" ("cha" + "ers") and "acters" ("act" + "ers").

```

**Example 3:**

```
Input: arr = ["abcdefghijklmnopqrstuvwxyz"]
Output: 26
Explanation: The only string in arr has all 26 characters.

```

**Constraints:**

- `1 <= arr.length <= 16`
- `1 <= arr[i].length <= 26`
- `arr[i]` contains only lowercase English letters.

```java
class Solution {
    int maxLen = 0;
    StringBuilder sb = new StringBuilder();

    public int maxLength(List<String> arr) {
        dfs(arr, 0);
        return maxLen;
    }

    private void dfs(List<String> arr, int index) {
        char[] chars = sb.toString().toCharArray();
        Set<Character> s = new HashSet<>();
        // 透過set判斷unique
        for(char c: chars) {
            if(s.contains(c)) return;
            else s.add(c);
        }
        // 計算最大長度
        maxLen = Math.max(maxLen, sb.length());
        // 遍歷資料組合
        for(int i = index; i < arr.size(); i++) {
            sb.append(arr.get(i));
            dfs(arr, i + 1);
            sb.delete(sb.length() - arr.get(i).length(), sb.length());
        }
    }

}
```