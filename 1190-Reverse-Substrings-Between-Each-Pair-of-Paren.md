# 1190. Reverse Substrings Between Each Pair of Parentheses

Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `s` that consists of lower case English letters and brackets.

Reverse the strings in each pair of matching parentheses, starting from the innermost one.

Your result should **not** contain any brackets.

**Example 1:**

```
Input: s = "(abcd)"
Output: "dcba"

```

**Example 2:**

```
Input: s = "(u(love)i)"
Output: "iloveu"
Explanation: The substring "love" is reversed first, then the whole string is reversed.

```

**Example 3:**

```
Input: s = "(ed(et(oc))el)"
Output: "leetcode"
Explanation: First, we reverse the substring "oc", then "etco", and finally, the whole string.

```

**Constraints:**

- `1 <= s.length <= 2000`
- `s` only contains lower case English characters and parentheses.
- It is guaranteed that all parentheses are balanced.

```java
class Solution {
    public String reverseParentheses(String s) {
        // u evol i
        Stack<String> st = new Stack<>();
        int i = 0;
        for (char c : s.toCharArray()) {
            String e = String.valueOf(c);
            if (")".equals(e)) {
                StringBuilder sb = new StringBuilder();
                while (!st.isEmpty() && !st.peek().equals("(")) {
                    StringBuilder sub = new StringBuilder(st.pop());
                    sb.append(sub.reverse().toString());
                }
                st.pop();// 丟掉(
                if (st.isEmpty() && i == s.length() - 1)
                    return sb.toString();// 做完
                else
                    st.push(sb.toString());// 還有剩
            } else {
                st.push(e);
            }
            i++;
        }
        // 最外層沒括號
        StringBuilder sb = new StringBuilder();
        while (!st.isEmpty() && !st.peek().equals("(")) {
            StringBuilder sub = new StringBuilder(st.pop());
            sb.append(sub.reverse().toString());
        }
        return sb.reverse().toString();
    }
}
```