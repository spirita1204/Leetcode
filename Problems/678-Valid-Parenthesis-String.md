# 678. Valid Parenthesis String

Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Given a string `s` containing only three types of characters: `'('`, `')'` and `'*'`, return `true` *if* `s` *is **valid***.

The following rules define a **valid** string:

- Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
- Any right parenthesis `')'` must have a corresponding left parenthesis `'('`.
- Left parenthesis `'('` must go before the corresponding right parenthesis `')'`.
- `'*'` could be treated as a single right parenthesis `')'` or a single left parenthesis `'('` or an empty string `""`.

**Example 1:**

```
Input: s = "()"
Output: true

```

**Example 2:**

```
Input: s = "(*)"
Output: true

```

**Example 3:**

```
Input: s = "(*))"
Output: true

```

**Constraints:**

- `1 <= s.length <= 100`
- `s[i]` is `'('`, `')'` or `'*'`.

```java
class Solution {
    public boolean checkValidString(String s) {
        Stack<Integer> openBrackets = new Stack<>();// 存(括號位址
        Stack<Integer> asterisks = new Stack<>();// 存星號位址，用於當需要時是否可補充

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(') {// '('
                openBrackets.push(i);
            } else if (c == ')') {// ')'
                if (!openBrackets.isEmpty()) {
                    openBrackets.pop();
                } else if (!asterisks.isEmpty()) {
                    asterisks.pop();
                } else {// 當沒有對應括號 且無星號做彌補時
                    return false;
                }
            } else {// '*'
                asterisks.push(i);
            }
        }
        while (!openBrackets.isEmpty() && !asterisks.isEmpty()) {
            // If an open bracket appears after an asterisk, it cannot be balanced, return false
            if (openBrackets.pop() > asterisks.pop()) {
                return false; // '*' before '(' which cannot be balanced.
            }
        }

        return openBrackets.isEmpty();
    }
}
```