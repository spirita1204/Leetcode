# 3612. Process String with Special Operations I  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given a string `s` consisting of lowercase English letters and the special characters: `*`, `#`, and `%`.

Build a new string `result` by processing `s` according to the following rules from left to right:  

- If the letter is a **lowercase** English letter append it to `result`.
- A `'*'` **removes** the last character from `result`, if it exists.
- A `'#'` **duplicates** the current `result` and **appends** it to itself.
- A `'%'` **reverses** the current `result`.
Return the final string `result` after processing all characters in `s`.

**Example 1:**

**Input:** s = "a#b%*"

**Output:** "ba"

**Explanation:**

Thus, the final `result` is `"ba"`.

**Example 2:**

**Input:** s = "z*#"

**Output:** ""   

**Explanation:**

Thus, the final `result` is `""`.

**Constraints:**

- `1 <= s.length <= 20`
- `s` consists of only lowercase English letters and special characters , `#`, and `%`.
```java
class Solution {
    public String processStr(String s) {
        StringBuilder sb = new StringBuilder();
        int n = s.length();

        for (int i = 0; i < n; i++) {
            char ch = s.charAt(i);

            if (ch == '*') {
                if (sb.length() != 0) {
                    sb.deleteCharAt(sb.length() - 1);
                }
            } 
            else if (ch == '#') {
                sb.append(sb);
            } 
            else if (ch == '%') {
                sb.reverse();
            } 
            else if (ch >= 'a' && ch <= 'z') {
                sb.append(ch);
            }
        }

        return sb.toString();
    }
}
```



