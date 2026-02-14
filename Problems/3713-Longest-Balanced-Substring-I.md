# 3713. Longest Balanced Substring I  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given a string `s` consisting of lowercase English letters.

A **substring** of `s` is called **balanced** if all **distinct** characters in the **substring** appear the **same** number of times.

Return the **length** of the **longest balanced substring** of `s`.

**Example 1:**

**Input:** s = "abbac"

**Output:** 4

**Explanation:**

The longest balanced substring is `"abba"` because both distinct characters `'a'` and `'b'` each appear exactly 2 times.

**Example 2:**

**Input:** s = "zzabccy"

**Output:** 4

**Explanation:**

The longest balanced substring is `"zabc"` because the distinct characters `'z'`, `'a'`, `'b'`, and `'c'` each appear exactly 1 time.

**Example 3:**

**Input:** s = "aba"

**Output:** 2

**Explanation:**

One of the longest balanced substrings is `"ab"` because both distinct characters `'a'` and `'b'` each appear exactly 1 time. Another longest balanced substring is `"ba"`.

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consists of lowercase English letters.
```java
class Solution {
    public int longestBalanced(String s) {
        int n = s.length();
        // 字串轉成數字陣列
        int[] a = new int[n];
        for (int i = 0; i < n; i++) 
            a[i] = s.charAt(i) - 'a';

        int result = 0;
        // 枚舉所有子字串起點
        for (int l = 0; l < n; l++) {
            if (n - l <= result) // 剪枝
                break;

            int[] cnt = new int[26]; 
            int uniq = 0, maxfreq = 0; 
            // 枚舉子字串結尾
            for (int r = l; r < n; r++) {
                int i = a[r];
                // s[l ... r]
                if (cnt[i] == 0) 
                    uniq++;

                cnt[i]++;
                // 更新 最大值 頻率
                if (cnt[i] > maxfreq) 
                    maxfreq = cnt[i];
                // uniq * maxfreq 
                int cur = r - l + 1;
                if (uniq * maxfreq == cur && cur > result)
                    result = cur;
            }
        }
        return result;
    }
}
```

