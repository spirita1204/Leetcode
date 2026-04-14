# 2840. Check if Strings Can be Made Equal With Operations II  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given two strings `s1` and `s2`, both of length `n`, consisting of **lowercase** English letters.        

You can apply the following operation on **any** of the two strings **any** number of times:

- Choose any two indices `i` and `j` such that `i < j` and the difference `j - i` is **even**, then **swap** the two characters at those indices in the string.
Return `true`* if you can make the strings *`s1`* and *`s2`* equal, and *`false`* otherwise*.

**Example 1:**

```plain text
Input: s1 = "abcdba", s2 = "cabdab"
Output: true
Explanation: We can apply the following operations on s1:
- Choose the indices i = 0, j = 2. The resulting string is s1 = "cbadba".
- Choose the indices i = 2, j = 4. The resulting string is s1 = "cbbdaa".  
- Choose the indices i = 1, j = 5. The resulting string is s1 = "cabdab" = s2.    
```

**Example 2:**

```plain text
Input: s1 = "abe", s2 = "bea"
Output: false  
Explanation: It is not possible to make the two strings equal.
```

**Constraints:   **

- `n == s1.length == s2.length`
- `1 <= n <= 105`
- `s1` and `s2` consist only of lowercase English letters.   
```java
class Solution {
    public boolean checkStrings(String s1, String s2) {
        int n = s1.length();               // = s2.length()
        // 26 個英文字母的頻率
        int[] even1 = new int[26];
        int[] odd1  = new int[26];
        int[] even2 = new int[26];
        int[] odd2  = new int[26];

        for (int i = 0; i < n; i++) {
            int c1 = s1.charAt(i) - 'a';
            int c2 = s2.charAt(i) - 'a';
            if ((i & 1) == 0) {            // 偶數位
                even1[c1]++;   
                even2[c2]++;
            } else {                       // 奇數位
                odd1[c1]++; 
                odd2[c2]++;
            }   
        }       

        // 檢查兩個奇偶集合是否完全相同
        for (int k = 0; k < 26; k++) {
            if (even1[k] != even2[k] || odd1[k] != odd2[k]) {
                return false;
            }
        }
        return true;
    }
}
```

