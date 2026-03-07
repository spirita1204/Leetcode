# 1784. Check if Binary String Has at Most One Segment of Ones  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given a binary string `s` **without leading zeros**, return `true` *if *`s`* contains ****at most one contiguous segment of ones***. Otherwise, return `false`.

**Example 1:**

```plain text
Input: s = "1001"
Output: false
Explanation:The ones do not form a contiguous segment.
```

**Example 2:**

```plain text
Input: s = "110"
Output: true   
```

**Constraints:   **

- `1 <= s.length <= 100`
- `s[i]` is either `'0'` or `'1'`.
- `s[0]` is `'1'`.
```java
class Solution {
    public boolean checkOnesSegment(String s) {
        return !s.contains("01");
    }
}
```

