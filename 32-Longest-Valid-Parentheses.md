# 32. Longest Valid Parentheses

Data structure: Stack
Difficulty: Hard

Hard

Topics

Companies

Given a string containing just the characters `'('` and `')'`, return *the length of the longest valid (well-formed) parentheses*

*substring*

.

**Example 1:**

```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".

```

**Example 2:**

```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".

```

**Example 3:**

```
Input: s = ""
Output: 0

```

**Constraints:**

- `0 <= s.length <= 3 * 104`
- `s[i]` is `'('`, or `')'`.

```java
class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> st = new Stack<>();
        int[] arr = new int[s.length()]; // 當有配對 擺1 計算最長相連1;
        int i = 0;

        for(char c: s.toCharArray()) {
            if(c == '(') st.push(i);
            else {
                if(!st.isEmpty()) {
                    int pre = st.pop();
                    arr[pre] = 1;
                    arr[i] = 1;
                }
            }
            i++;
        }
        int max = 0;
        int now = 0;
        for(int one: arr) {
            if(one == 1) now++;
            else {
                max = Math.max(max, now);
                now = 0;
            }
        }
        max = Math.max(max, now);

        return max;
    }
}
```