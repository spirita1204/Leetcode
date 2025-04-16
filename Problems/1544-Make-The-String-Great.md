# 1544. Make The String Great  

  Methods: Bitwise </br> Difficulty: Easy </br> </br>Given a string `s` of lower and upper case English letters.

A good string is a string which doesn't have **two adjacent characters** `s[i]` and `s[i + 1]` where:

- `0 <= i <= s.length - 2`
- `s[i]` is a lower-case letter and `s[i + 1]` is the same letter but in upper-case or **vice-versa**.
To make the string good, you can choose **two adjacent** characters that make the string bad and remove them. You can keep doing this until the string becomes good.

Return *the string* after making it good. The answer is guaranteed to be unique under the given constraints.

**Notice** that an empty string is also good.

**Example 1:**

```plain text
Input: s = "leEeetcode"
Output: "leetcode"
Explanation: In the first step, either you choose i = 1 or i = 2, both will result "leEeetcode" to be reduced to "leetcode".

```

**Example 2:**

```plain text
Input: s = "abBAcC"
Output: ""
Explanation: We have many possible scenarios, and all lead to the same answer. For example:
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""

```

**Example 3:**

```plain text
Input: s = "s"
Output: "s"

```

**Constraints:**

- `1 <= s.length <= 100`
- `s` contains only lower and upper case English letters.
```java
class Solution {
    public String makeGood(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            int lenght = sb.length();
            // we check if the last character is same letter but in upper-case or vice-versa
            // here we can use XOR and 1 << 5 to convert a lower character to a upper one
            // and vice-versa
            // A: 01[0]00001 差32位
            // a: 01[1]00001
            // Z: 01[0]11010
            // z: 01[1]11010
            // a -> A / A -> a
            if (lenght > 0 && ((sb.charAt(lenght - 1) ^ (1 << 5)) == s.charAt(i))) {// XOR
                // if it matches the requirement, we remove the last character in `sb`
                sb.deleteCharAt(lenght - 1);
            } else {
                // otherwise, we add the current char to `sb`
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

