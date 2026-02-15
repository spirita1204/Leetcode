# 3714. Longest Balanced Substring II  

  Methods: Prefix Sum </br> Difficulty: Medium,Medium++ </br> </br>You are given a string `s` consisting only of the characters `'a'`, `'b'`, and `'c'`.

A **substring** of `s` is called **balanced** if all **distinct** characters in the **substring** appear the **same** number of times.

Return the **length of the longest balanced substring** of `s`.

**Example 1:**

**Input:** s = "abbac"

**Output:** 4

**Explanation:**

The longest balanced substring is `"abba"` because both distinct characters `'a'` and `'b'` each appear exactly 2 times.

**Example 2:**

**Input:** s = "aabcc"

**Output:** 3

**Explanation:**

The longest balanced substring is `"abc"` because all distinct characters `'a'`, `'b'` and `'c'` each appear exactly 1 time.

**Example 3:**

**Input:** s = "aba"

**Output:** 2

**Explanation:**

One of the longest balanced substrings is `"ab"` because both distinct characters `'a'` and `'b'` each appear exactly 1 time. Another longest balanced substring is `"ba"`.

**Constraints:**

- `1 <= s.length <= 105`
- `s` contains only the characters `'a'`, `'b'`, and `'c'`.
```java
class Solution {
    public int longestBalanced(String s) {
        char[] c = s.toCharArray();
        int n = c.length;
        // 如果字串只包含 a, b, c，那麼 balanced 可能有：
        // 只包含 1 種字母（aaaa）
        // 包含 2 種字母，且次數相等（aabb）   
        // 包含 3 種字母，且次數相等（abcabc）
        int cur_a = 0, cur_b = 0, cur_c = 0;        
        int max_a = 0, max_b = 0, max_c = 0;
        // 1. 只包含 1 種字母（aaaa）
        for (int i = 0; i < n; i++) {
            if (c[i] == 'a') {
                cur_a = (i > 0 && c[i-1] == 'a') ? cur_a + 1 : 1;
                max_a = Math.max(max_a, cur_a);
            } else if (c[i] == 'b') {
                cur_b = (i > 0 && c[i-1] == 'b') ? cur_b + 1 : 1;
                max_b = Math.max(max_b, cur_b);
            } else { 
                cur_c = (i > 0 && c[i-1] == 'c') ? cur_c + 1 : 1;
                max_c = Math.max(max_c, cur_c);
            }  
        }
        
        int res = Math.max(Math.max(max_a, max_b), max_c);
        // 2.包含 2 種字母，且次數相等（aabb）
        res = Math.max(res, find2(c, 'a', 'b'));
        res = Math.max(res, find2(c, 'a', 'c'));
        res = Math.max(res, find2(c, 'b', 'c'));
        // 3.包含 3 種字母，且次數相等（abcabc）
        res = Math.max(res, find3(c));
        
        return res;
    }
    
    // count(x) == count(y) prefix sum 
    private int find2(char[] c, char x, char y) {
        int n = c.length, max_len = 0;
        // diff = count(x) - count(y)
        // first: 某個 diff 第一次出現的位置
        int[] first = new int[2 * n + 1];// count(x) - count(y)可能 -n ~ +n
        Arrays.fill(first, -2);
        
        int clear_idx = -1, diff = n;
        first[diff] = -1;
        for (int i = 0; i < n; i++) {      
            // 例如現在處理 (a,b)，卻遇到 c 必須「重新開始」，
            if (c[i] != x && c[i] != y) {
                clear_idx = i;
                diff = n;
                first[diff] = clear_idx;
            } else {
                if (c[i] == x) diff++;
                else diff--;
                // 如果這個 diff 第一次出現 → 記錄位置
                // 如果已經出現過 → 找到一段平衡區間
                if (first[diff] < clear_idx) {
                    first[diff] = i;
                } else {
                    max_len = Math.max(max_len, i - first[diff]);
                }
            }
        }
        
        return max_len;
    }
    // 狀態壓縮
    private int find3(char[] c) {
        long state = Long.MAX_VALUE / 2;
        Map<Long, Integer> first = new HashMap<>();
        first.put(state, -1);
    
        int max_len = 0;
        // count(a) == count(b) == count(c)
        for (int i = 0; i < c.length; i++) {
            // (a-b, b-c) 的組合唯一對應一個 state
            if (c[i] == 'a') state += 1_000_001;
            else if (c[i] == 'b') state -= 1_000_000;
            else state--;
            // state = (a-b) * 1_000_000 + (b-c)
            if (first.containsKey(state)) {
                max_len = Math.max(max_len, i - first.get(state));
            } else {
                first.put(state, i);
            }
        }
    
        return max_len;
    }
}
```

