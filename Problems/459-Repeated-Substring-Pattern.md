# 459. Repeated Substring Pattern  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given a string `s`, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.  

**Example 1:**

```plain text
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.
```

**Example 2:**

```plain text
Input: s = "aba"
Output: false
```

**Example 3:**

```plain text
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.
```

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of lowercase English letters.
```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int len = s.length();
        
        for(int i = 1; i <= len / 2; i++) {
            if(len % i == 0) {
                String sub = s.substring(0, i);
                StringBuilder sb = new StringBuilder();
                for(int j = 0; j < len / i; j++) 
                    sb.append(sub);
    
                if(s.equals(sb.toString()))
                    return true;
            }
        }
        return false;
    }
}
```

