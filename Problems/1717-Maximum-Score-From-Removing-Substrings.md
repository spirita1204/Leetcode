# 1717. Maximum Score From Removing Substrings

Methods: Greedy
Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `s` and two integers `x` and `y`. You can perform two types of operations any number of times.

- Remove substring `"ab"` and gain `x` points.
    - For example, when removing `"ab"` from `"cabxbae"` it becomes `"cxbae"`.
- Remove substring `"ba"` and gain `y` points.
    - For example, when removing `"ba"` from `"cabxbae"` it becomes `"cabxe"`.

Return *the maximum points you can gain after applying the above operations on* `s`.

**Example 1:**

```
Input: s = "cdbcbbaaabab", x = 4, y = 5
Output: 19
Explanation:
- Remove the "ba" underlined in "cdbcbbaaabab". Now, s = "cdbcbbaaab" and 5 points are added to the score.
- Remove the "ab" underlined in "cdbcbbaaab". Now, s = "cdbcbbaa" and 4 points are added to the score.
- Remove the "ba" underlined in "cdbcbbaa". Now, s = "cdbcba" and 5 points are added to the score.
- Remove the "ba" underlined in "cdbcba". Now, s = "cdbc" and 5 points are added to the score.
Total score = 5 + 4 + 5 + 5 = 19.
```

**Example 2:**

```
Input: s = "aabbaaxybbaabb", x = 5, y = 4
Output: 20

```

**Constraints:**

- `1 <= s.length <= 105`
- `1 <= x, y <= 104`
- `s` consists of lowercase English letters.

```java
class Solution {
    public int maximumGain(String s, int x, int y) {
        Stack<Character> st = new Stack<>();
        int sum = 0;
        int choose = (x > y)? 1: 2;
        // 做兩次 x來回
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(choose == 1){
                if(!st.isEmpty() && st.peek() == 'a' && c == 'b') {
                    st.pop();
                    sum += x;
                }
                else st.push(c);
            } else {
                if(!st.isEmpty() && st.peek() == 'b' && c == 'a') {
                    st.pop();
                    sum += y;
                }
                else st.push(c);
            }
        }
        // 一次取一個出來 需處理bbaa,aabb情境
        Stack<Character> st2 = new Stack<>();
        while(!st.isEmpty()) {
            char c = st.pop();
            if(choose == 1){
                if(!st2.isEmpty() && st2.peek() == 'a' && c == 'b') {
                    st2.pop();
                    sum += y;
                }
                else st2.push(c);
            } else {
                if(!st2.isEmpty() && st2.peek() == 'b' && c == 'a') {
                    st2.pop();
                    sum += x;
                }
                else st2.push(c);
            }
        }
        return sum;
    }
    // cbaabwbbbabbwaaq x=4074 y=9819
    //  ____   __ x+2y=4074+19638=23712
}
```