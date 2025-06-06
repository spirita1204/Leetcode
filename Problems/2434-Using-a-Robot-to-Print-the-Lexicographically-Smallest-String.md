# 2434. Using a Robot to Print the Lexicographically Smallest String  

  Data Structure: Stack </br> Difficulty: Medium </br> </br>You are given a string `s` and a robot that currently holds an empty string `t`. Apply one of the following operations until `s` and `t` **are both empty**: 

- Remove the **first** character of a string `s` and give it to the robot. The robot will append this character to the string `t`.
- Remove the **last** character of a string `t` and give it to the robot. The robot will write this character on paper.
Return *the lexicographically smallest string that can be written on the paper.*

**Example 1:**

```plain text
Input: s = "zza"
Output: "azz"
Explanation: Let p denote the written string.
Initially p="", s="zza", t="".
Perform first operation three times p="", s="", t="zza".
Perform second operation three times p="azz", s="", t="".
```

**Example 2:**

```plain text
Input: s = "bac"
Output: "abc"
Explanation: Let p denote the written string.
Perform first operation twice p="", s="c", t="ba".
Perform second operation twice p="ab", s="c", t="".
Perform first operation p="ab", s="", t="c".
Perform second operation p="abc", s="", t="".
```

**Example 3:**

```plain text
Input: s = "bdda"
Output: "addb"
Explanation: Let p denote the written string.
Initially p="", s="bdda", t="".
Perform first operation four times p="", s="", t="bdda".
Perform second operation four times p="addb", s="", t="".
```

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only English lowercase letters.
```java
class Solution {
    public String robotWithString(String s) {
        Stack<Character> st = new Stack<>();
        StringBuilder sb = new StringBuilder();
        int[] freq = new int[26];
        
        for (char c : s.toCharArray()) 
            freq[c - 'a']++;
        

        for (char c : s.toCharArray()) {
            st.push(c);
            freq[c - 'a']--;

            while (!st.isEmpty() && st.peek() <= smallestChar(freq)) 
                sb.append(st.pop());
        }

        while (!st.isEmpty()) 
            sb.append(st.pop());

        return sb.toString();
    }

    private char smallestChar(int[] freq) {
        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0) {
                return (char) ('a' + i);
            }
        }
        return 'a';
    }
}
```

