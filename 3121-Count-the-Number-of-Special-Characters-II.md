# 3121. Count the Number of Special Characters II

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a string `word`. A letter `c` is called **special** if it appears **both** in lowercase and uppercase in `word`, and **every** lowercase occurrence of `c` appears before the **first** uppercase occurrence of `c`.

Return the number of ****special** letters **in **`word`.

**Example 1:**

**Input:** word = "aaAbcBC"

**Output:** 3

**Explanation:**

The special characters are `'a'`, `'b'`, and `'c'`.

**Example 2:**

**Input:** word = "abc"

**Output:** 0

**Explanation:**

There are no special characters in `word`.

**Example 3:**

**Input:** word = "AbBCab"

**Output:** 0

**Explanation:**

There are no special characters in `word`.

**Constraints:**

- `1 <= word.length <= 2 * 105`
- `word` consists of only lowercase and uppercase English letters.

```java
class Solution {
    public int numberOfSpecialChars(String word) { 
        char[] crrs = new char[26];
        int res = 0;

        for(char c: word.toCharArray()) {
            if(Character.isUpperCase(c)) {// 大寫需判斷是否已有小寫
                char lowerC = Character.toLowerCase(c);
                if(crrs[lowerC - 'a'] == lowerC) {
                    crrs[lowerC - 'a'] = c;// 小寫變大寫
                } else if(crrs[lowerC - 'a'] == c) {// 大寫碰大寫
                    //
                } else {// 前面沒小寫
                    crrs[lowerC - 'a'] = '0';// 0代表以後都沒用
                }
            } else {// 小寫
                char UpperC = Character.toUpperCase(c);
                if(crrs[c - 'a'] == UpperC) {// 當前已經有大寫 須扣回
                    crrs[c - 'a'] = '0';
                } else {
                    if(crrs[c - 'a'] != '0')
                        crrs[c - 'a'] = c;
                }
            }
        }
        for(char c: crrs) 
            if(Character.isUpperCase(c))    
                res++;

        return res;
    }
}
```