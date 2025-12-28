# 3234. Count the Number of Substrings With Dominant Ones  

  Methods: Prefix Sum,Sliding Window </br> Difficulty: Medium </br> </br>You are given a binary string `s`.

Return the number of substrings with **dominant** ones.

A string has **dominant** ones if the number of ones in the string is **greater than or equal to** the **square** of the number of zeros in the string.

**Example 1:**

**Input:** s = "00011"

**Output:** 5

**Explanation:**

The substrings with dominant ones are shown in the table below.

**Example 2:**

**Input:** s = "101101"

**Output:** 16

**Explanation:   **

The substrings with **non-dominant** ones are shown in the table below.

Since there are 21 substrings total and 5 of them have non-dominant ones, it follows that there are 16 substrings with dominant ones.  

**Constraints:**

- `1 <= s.length <= 4 * 104`
- `s` consists only of characters `'0'` and `'1'`.
```java
class Solution {
    public int numberOfSubstrings(String s) {
        // Prefix Sum 快速算 1 的數量
        // 固定起點 i，往右擴 j
        // 利用數學性質「提前跳過 j」避免無效檢查
        int n = s.length(); 
        int[] prefix = new int[n]; // prefix sums of '1's

        prefix[0] = ((s.charAt(0) - '0')) == 1 ? 1 : 0;
        for (int i = 1; i < n; i++) 
            prefix[i] = prefix[i - 1] + (((s.charAt(i) - '0')) == 1 ? 1 : 0);

        int ans = 0;
 
        for (int i = 0; i < n; i++) { //i => starting index of substring
            int one = 0; // Count of '1's in the current substring
            int zero = 0; // Count of '0's in the current substring
            for (int j = i; j < n; j++) { // j=> ending index of current substring
                one = prefix[j] - (i == 0 ? 0 : prefix[i - 1]);
                zero = (j - i + 1) - one;
              
                //CASE->1
                if ((zero * zero) > one) { // Not dominant
                    j += (zero * zero - one - 1);// 跳 -> 中間都不合法 避免TLE
                } 
                //CASE->2
                else if ((zero * zero) == one) { //just this one is dominant
                    ans++; 
                } 
                //CASE->3
                else if ((zero * zero) < one) { 
                    ans++; 
                    // Calculate the difference to determine how far to skip forward
                    int diff = (int) Math.sqrt(one) - zero;
                    int nextj = j + diff; // Determine the next position to skip to

                    if (nextj >= n) {
                        ans += (n - j - 1);
                    } else {
                        ans += diff; 
                    }

                    j = nextj; // Update j to the next position
                }
            }
        }
        return ans; // Return the final answer
    }
}
```

