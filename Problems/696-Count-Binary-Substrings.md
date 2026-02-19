# 696. Count Binary Substrings  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given a binary string `s`, return the number of non-empty substrings that have the same number of `0`'s and `1`'s, and all the `0`'s and all the `1`'s in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

**Example 1:**

```plain text
Input: s = "00110011"
Output: 6
Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".
Notice that some of these substrings repeat and are counted the number of times they occur.
Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.
```

**Example 2:**

```plain text
Input: s = "10101"
Output: 4
Explanation: There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.
```

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either `'0'` or `'1'`.
```java
class Solution {
    public int countBinarySubstrings(String s) {
        // tip: Eg: "00011100" --> [3 zeroes, 3 ones, 2 zeroes] --> [3,3,2] 
        //      --> Ans = min(3,3) + min(3,2) = 5 Total Substrings
        List<Integer> list = new ArrayList<>();
        boolean zero = false;
        int cnt = 1;
        zero = (s.charAt(0) == '0');

        for(int i = 1; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c == '0' && zero || c == '1' && !zero) {
                cnt++;
            } else {
                zero = !zero;
                list.add(cnt);
                cnt = 1;
            } 
        }
        list.add(cnt);

        int res = 0;
        for(int i = 1; i < list.size(); i++) {
            res += Math.min(list.get(i), list.get(i - 1));
        }
        return res;
    }
}
```

