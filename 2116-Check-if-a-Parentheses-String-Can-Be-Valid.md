# 2116. Check if a Parentheses String Can Be Valid

Methods: Greedy
Data structure: Stack
Difficulty: Medium
Similar: 678

https://www.youtube.com/watch?v=4YK8WrE-ssQ

A parentheses string is a **non-empty** string consisting only of `'('` and `')'`. It is valid if **any** of the following conditions is **true**:

- It is `()`.
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid parentheses strings.
- It can be written as `(A)`, where `A` is a valid parentheses string.

You are given a parentheses string `s` and a string `locked`, both of length `n`. `locked` is a binary string consisting only of `'0'`s and `'1'`s. For **each** index `i` of `locked`,

- If `locked[i]` is `'1'`, you **cannot** change `s[i]`.
- But if `locked[i]` is `'0'`, you **can** change `s[i]` to either `'('` or `')'`.

Return `true` *if you can make `s` a valid parentheses string*. Otherwise, return `false`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/11/06/eg1.png](https://assets.leetcode.com/uploads/2021/11/06/eg1.png)

```
Input: s = "))()))", locked = "010100"
Output: true
Explanation: locked[1] == '1' and locked[3] == '1', so we cannot change s[1] or s[3].
We change s[0] and s[4] to '(' while leaving s[2] and s[5] unchanged to make s valid.
```

**Example 2:**

```
Input: s = "()()", locked = "0000"
Output: true
Explanation: We do not need to make any changes because s is already valid.

```

**Example 3:**

```
Input: s = ")", locked = "0"
Output: false
Explanation: locked permits us to change s[0].
Changing s[0] to either '(' or ')' will not make s valid.

```

**Constraints:**

- `n == s.length == locked.length`
- `1 <= n <= 105`
- `s[i]` is either `'('` or `')'`.
- `locked[i]` is either `'0'` or `'1'`.

```java
class Solution {
    public boolean canBeValid(String s, String locked) {
        if(s.length() % 2 != 0)
            return false;
        Stack<Integer> openBrackets = new Stack<>();// 存(括號位址
        Stack<Integer> asterisks = new Stack<>();// 存星號位址，用於當需要時是否可補充

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(locked.charAt(i) == '0')
                c = '*';
            //////
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