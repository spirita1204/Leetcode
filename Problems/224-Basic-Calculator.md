# 224. Basic Calculator

Data structure: Stack
Difficulty: Hard

Hard

Topics

Companies

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return *the result of the evaluation*.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**

```
Input: s = "1 + 1"
Output: 2

```

**Example 2:**

```
Input: s = " 2-1 + 2 "
Output: 3

```

**Example 3:**

```
Input: s = "(1+(4+5+2)-3)+(6+8)"
Output: 23

```

**Constraints:**

- `1 <= s.length <= 3 * 105`
- `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
- `s` represents a valid expression.
- `'+'` is **not** used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` is invalid).
- `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` is valid).
- There will be no two consecutive operators in the input.
- Every number and running calculation will fit in a signed 32-bit integer.

```java
class Solution {
    public int calculate(String s) {
        Stack<Integer> st = new Stack<>();// 數字
        int result = 0;
        int sign = 1;

        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if(Character.isDigit(c)) {// 數字
                int sum = c - '0';
                while (i + 1 < s.length() && Character.isDigit(s.charAt(i + 1))) {// 多位數
							    sum = sum * 10 + (s.charAt(i + 1) - '0');
							    i++;
						    }
						    result += sum * sign;
            } else {// 符號
                if(c == '+') sign = 1;
                if(c == '-') sign = -1;
                if(c == '(') {
                    st.push(result);
                    st.push(sign);
                    result = 0;// init
                    sign = 1;// init
                }
                if(c == ')')  result = result * st.pop() + st.pop();// (值)* sign + 前(值)
            }
        }
        return result;
    }
}
```