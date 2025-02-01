# 227. Basic Calculator II  

  Data Structure: Stack </br> Difficulty: Medium </br> </br>Given a string `s` which represents an expression, *evaluate this expression and return its value*.

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**

```plain text
Input: s = "3+2*2"
Output: 7

```

**Example 2:**

```plain text
Input: s = " 3/2 "
Output: 1

```

**Example 3:**

```plain text
Input: s = " 3+5 / 2 "
Output: 5

```

**Constraints:**

- `1 <= s.length <= 3 * 105`
- `s` consists of integers and operators `('+', '-', '*', '/')` separated by some number of spaces.
- `s` represents **a valid expression**.
- All the integers in the expression are non-negative integers in the range `[0, 231 - 1]`.
- The answer is **guaranteed** to fit in a **32-bit integer**.
```java
class Solution {
    public int calculate(String s) {
        s = s.replaceAll(" ", "");
        Stack<Integer> st = new Stack<>();// 數字
        Stack<Character> st2 = new Stack<>();// 符號
        int sign = 1;

        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (!Character.isDigit(c)) {// 符號
                if(c == '+') sign = 1;
                if(c == '-') sign = -1;
                st2.push(c);
            } else {// 數字
                int sum = c - '0';
                while (i + 1 < s.length() && Character.isDigit(s.charAt(i + 1))) {// 多位數
                    sum = sum * 10 + (s.charAt(i + 1) - '0');
                    i++;
                }
                sum *= sign;
                if (!st2.isEmpty() && (st2.peek() == '/' || st2.peek() == '*')) {
                    int a = st.pop();
                    int b = sum;
                    int res = calculate(a, b, st2.pop());
                    if(!st2.isEmpty() && st2.peek() == '-')
                        st.push(res * -1);
                    else 
                        st.push(res);
                } else {
                    st.push(sum);
                }
            }
        }
        if(st2.isEmpty())
            return st.pop();
        int res = 0;
        while(!st2.isEmpty()) {
            int b = st.pop();
            int a = st.pop();
            int sum = calculate(a, b, st2.pop());
            res = sum;
            st.push(sum);
        }
        return res;
    }

    private int calculate(int a, int b, char c) {
        if (c == '+' || c == '-')// 因為-由sign處理掉
            return a + b;
        if (c == '*')
            return a * b;
        return a / b;
    }
}
```

