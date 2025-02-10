# 3174. Clear Digits  

  Data Structure: Stack </br> Difficulty: Easy </br> </br>You are given a string `s`.

Your task is to remove **all** digits by doing this operation repeatedly:

- Delete the *first* digit and the **closest** **non-digit** character to its *left*.
Return the resulting string after removing all digits.

**Example 1:**

```java
Input: s = "abc"
Output: "abc"
Explanation: There is no digit in the string.
```

Example 2:
```java
Input: s = "cb34"
Output: ""
Explanation:
First, we apply the operation on `s[2]`, and `s` becomes `"c4"`.
Then we apply the operation on `s[1]`, and `s` becomes `""`.
```
**Constraints:**

- `1 <= s.length <= 100`
- `s` consists only of lowercase English letters and digits.
- The input is generated such that it is possible to delete all digits.
```java
class Solution {
    public String clearDigits(String s) {
        StringBuilder sb = new StringBuilder();

        for(char c: s.toCharArray()) {
            if(!Character.isDigit(c)) 
                sb.append(c);
            else 
                sb.deleteCharAt(sb.length() - 1);
        }
        return sb.toString();
    }
}
```

