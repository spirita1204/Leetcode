# 1189. Maximum Number of Balloons  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given a string `text`, you want to use the characters of `text` to form as many instances of the word **"balloon"** as possible.

You can use each character in `text` **at most once**. Return the maximum number of instances that can be formed.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2019/09/05/1536_ex1_upd.JPG)

```plain text
Input: text = "nlaebolko"
Output: 1
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2019/09/05/1536_ex2_upd.JPG)

```plain text
Input: text = "loonbalxballpoon"
Output: 2
```

**Example 3:**

```plain text
Input: text = "leetcode"
Output: 0   
```

**Constraints:**

- `1 <= text.length <= 104`
- `text` consists of lower case English letters only.
**Note:** This question is the same as [2287: Rearrange Characters to Make Target String.](https://leetcode.com/problems/rearrange-characters-to-make-target-string/description/)

```java
class Solution {
    public int maxNumberOfBalloons(String s) {
        int[] f = new int[5];
        String t = "balon";

        for (int i = 0; i < s.length(); i++)
            for (int j = 0; j < 5; j++)
                if (s.charAt(i) == t.charAt(j))
                    f[j]++;

        f[2] >>= 1;
        f[3] >>= 1;

        return Arrays.stream(f).min().getAsInt();
    }
}
```



