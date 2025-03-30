# 763. Partition Labels  

  Methods: Greedy </br> Difficulty: Medium </br> </br>You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return *a list of integers representing the size of these parts*.

**Example 1:**

```plain text
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.
```

**Example 2:**

```plain text
Input: s = "eccbbbbdec"
Output: [10]
```

**Constraints:**

- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> res = new ArrayList<>();
        int[] hm = new int[26];
        // 將每一字母對應最後出現index 先記錄
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            hm[c- 'a'] = i;
        }
        // 透過 start, end去定位區間 看是否要延伸
        int start = 0, end = 0;
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            int last = hm[c - 'a'];// 取得最後索引
            end = Math.max(end, last);// 拓展
            if(i == end) {// 代表當前都在這區間
                res.add(end - start + 1);
                start = i + 1;
            }

        }
        return res;
    }
}
```

Python 

```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        res = []
        hm = [0] * 26

        # 將每個字母對應最後出現的索引位置先記錄下來
        for i, c in enumerate(s):
            hm[ord(c) - ord('a')] = i # ord -> ascii

        # 透過 start 和 end 來定位區間，看是否需要延伸
        start, end = 0, 0
        for i, c in enumerate(s):
            last = hm[ord(c) - ord('a')]  # 取得最後出現的索引位置
            end = max(end, last)  # 擴展 end
            if i == end:  # 若當前索引等於 end，則代表該區間內的字母都只出現在這個區間內
                res.append(end - start + 1)
                start = i + 1

        return res
```

