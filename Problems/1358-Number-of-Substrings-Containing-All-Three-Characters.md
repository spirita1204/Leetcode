# 1358. Number of Substrings Containing All Three Characters  

  Methods: Pointer </br> Difficulty: Medium </br> Similar: 3306 </br> </br>Given a string `s` consisting only of characters *a*, *b* and *c*.

Return the number of substrings containing **at least** one occurrence of all these characters *a*, *b* and *c*.

**Example 1:**

```plain text
Input: s = "abcabc"
Output: 10
Explanation: The substrings containing at least one occurrence of the charactersa,b andc are "abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab", "cabc"and "abc"(again).
```

**Example 2:**

```plain text
Input: s = "aaacb"
Output: 3
Explanation: The substrings containing at least one occurrence of the charactersa,b andc are "aaacb", "aacb"and "acb".
```

**Example 3:**

```plain text
Input: s = "abc"
Output: 1
```

**Constraints:**

- `3 <= s.length <= 5 x 10^4`
- `s` only consists of *a*, *b* or *c *characters.
```java
class Solution {
    public int numberOfSubstrings(String s) {
        String chars = "abc";
        int left = 0;// 兩個指標，控制滑動視窗
        int uniqueCount = 0; 
        int[] frequency = new int[3]; 
        int[] tempFrequency = new int[3]; 
        int res = 0; // 儲存符合條件的子字串數量

        // 使用 right 指標遍歷字串
        for (int right = 0; right < s.length(); right++) {
            int idx = chars.indexOf(s.charAt(right)); 
            frequency[idx]++; 

            if (frequency[idx] == 1) 
                uniqueCount++;
            // 檢查當前視窗是否符合條件
            if (uniqueCount == 3) {
                while (true) {
                    int midIndex = chars.indexOf(s.charAt(left));
                    if (frequency[midIndex] - tempFrequency[midIndex] == 1) 
                        break;
                    tempFrequency[midIndex]++; 
                    left++;
                }
                // 計算所有符合條件的子字串
                res += left - 0  + 1;
            }
        }
        return res;
    }
}
```

