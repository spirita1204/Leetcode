# 68. Text Justification

Methods: Basic logic
Difficulty: Hard

Hard

Topics

Companies

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**

- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.
- The input array `words` contains at least one word.

**Example 1:**

```
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

**Example 2:**

```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
```

**Example 3:**

```
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

**Constraints:**

- `1 <= words.length <= 300`
- `1 <= words[i].length <= 20`
- `words[i]` consists of only English letters and symbols.
- `1 <= maxWidth <= 100`
- `words[i].length <= maxWidth`

---

```java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        // 7 2 4 2 | 10 4 | 6 2 7 2 |
        List<String> res = new ArrayList<>();
        int row = 0;// 當前長度
        List<List<Integer>> lens = new ArrayList<>();
        List<List<Integer>> parts = new ArrayList<>();
        List<Integer> sub = new ArrayList<>();// 存每行每個元素長度
        List<Integer> part = new ArrayList<>();

        for (String s : words) {
            int strLen = s.length();
            if (row + strLen <= maxWidth) {
                sub.add(strLen);
            } else {
                lens.add(new ArrayList(sub));
                int n = maxWidth - row + 1 + (sub.size() - 1);
                int k = sub.size() - 1;
                interval(n, k == 0 ? 1 : k, part);
                parts.add(new ArrayList(part));
                // 換行
                part.clear();
                row = 0;
                sub.clear();
                sub.add(strLen);
            }
            row += (strLen + 1);
        }
        lens.add(new ArrayList(sub));
        if(part.size() != 0) 
            parts.add(new ArrayList(part));

        int i = 0;
        int nowRow = 0;
        for (List<Integer> pt : parts) {
            StringBuilder sb = new StringBuilder();
            for (int p : pt) {
                sb.append(words[i++]);
                appendSpaces(sb, p);
            }
            if(lens.get(nowRow++).size() != 1 && i < words.length)
                sb.append(words[i++]);
           
            res.add(sb.toString());
        }
        if(i < words.length){
            StringBuilder last = new StringBuilder();
            while(i < words.length) last.append(words[i++]).append(" ");
            int length = last.length();
            if(length > maxWidth) last.delete(maxWidth, length);
            appendSpaces(last, maxWidth - length);
            res.add(last.toString());
        }
    
        return res;
    }

    private void interval(int n, int k, List<Integer> parts) {
        // 你要切割的整数
        // 分成的等分数
        int quotient = n / k; // 整除部分
        int remainder = n % k; // 余数部分

        // 将整数n分成k等分
        for (int i = 0; i < k; i++) {
            if (remainder-- > 0) {
                parts.add(quotient + 1);
            } else {
                parts.add(quotient);
            }
        }
    }

    private void appendSpaces(StringBuilder sb, int count) {
        for (int i = 0; i < count; i++) {
            sb.append(' ');
        }
    }
}
```