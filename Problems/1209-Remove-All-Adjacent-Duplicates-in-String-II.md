# 1209. Remove All Adjacent Duplicates in String II

Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `s` and an integer `k`, a `k` **duplicate removal** consists of choosing `k` adjacent and equal letters from `s` and removing them, causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make `k` **duplicate removals** on `s` until we no longer can.

Return *the final string after all such duplicate removals have been made*. It is guaranteed that the answer is **unique**.

**Example 1:**

```
Input: s = "abcd", k = 2
Output: "abcd"
Explanation:There's nothing to delete.
```

**Example 2:**

```
Input: s = "deeedbbcccbdaa", k = 3
Output: "aa"
Explanation:
First delete "eee" and "ccc", get "ddbbbdaa"
Then delete "bbb", get "dddaa"
Finally delete "ddd", get "aa"
```

**Example 3:**

```
Input: s = "pbbcggttciiippooaais", k = 2
Output: "ps"

```

**Constraints:**

- `1 <= s.length <= 105`
- `2 <= k <= 104`
- `s` only contains lowercase English letters.

```java
class Solution {
    public String removeDuplicates(String s, int k) {
        Stack<CharCounter> st = new Stack<>();

        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (!st.isEmpty() && c == st.peek().c) {
                if (st.peek().count == k - 1) {
                    st.pop();
                } else {
                    st.peek().count++;
                }
            } else {
                st.push(new CharCounter(c));
            }
        }
        StringBuilder res = new StringBuilder();
        for (CharCounter charCount: st) {
            for(int i = 0; i < charCount.count; i++) {
                res.append(charCount.c);
            }       
        }
        return res.toString();
    }
}

class CharCounter {
    char c;
    int count;
    
    CharCounter(char c) {
        this.c = c;
        this.count = 1;
    }
}
```