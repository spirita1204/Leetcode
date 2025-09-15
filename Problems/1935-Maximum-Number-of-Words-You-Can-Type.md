# 1935. Maximum Number of Words You Can Type  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>There is a malfunctioning keyboard where some letter keys do not work. All other keys on the keyboard work properly.

Given a string `text` of words separated by a single space (no leading or trailing spaces) and a string `brokenLetters` of all **distinct** letter keys that are broken, return *the ****number of words**** in* `text` *you can fully type using this keyboard*.

**Example 1:**

```plain text
Input: text = "hello world", brokenLetters = "ad"
Output: 1
Explanation: We cannot type "world" because the 'd' key is broken.
```

**Example 2:**

```plain text
Input: text = "leet code", brokenLetters = "lt"
Output: 1
Explanation: We cannot type "leet" because the 'l' and 't' keys are broken.
```

**Example 3:**

```plain text
Input: text = "leet code", brokenLetters = "e"
Output: 0
Explanation: We cannot type either word because the 'e' key is broken.
```

**Constraints:**

- `1 <= text.length <= 104`
- `0 <= brokenLetters.length <= 26`
- `text` consists of words separated by a single space without any leading or trailing spaces.
- Each word only consists of lowercase English letters.
- `brokenLetters` consists of **distinct** lowercase English letters.
```java
class Solution {
    public int canBeTypedWords(String text, String brokenLetters) {
        String[] arr = text.split(" ");
        int ans = arr.length;

        for(int i = 0; i < arr.length; i++) {
            String s = arr[i];
            for(char c: brokenLetters.toCharArray()) {
                if(s.contains(String.valueOf(c))) {
                    ans--;
                    break;
                }
            }
        }
        return ans;
    }
}
```

