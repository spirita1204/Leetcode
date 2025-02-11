# 784. Letter Case Permutation

Methods: DFS
Difficulty: Medium

Given a string `s`, you can transform every letter individually to be lowercase or uppercase to create another string.

Return *a list of all possible strings we could create*. Return the output in **any order**.

**Example 1:**

```
Input: s = "a1b2"
Output: ["a1b2","a1B2","A1b2","A1B2"]

```

**Example 2:**

```
Input: s = "3z4"
Output: ["3z4","3Z4"]

```

**Constraints:**

- `1 <= s.length <= 12`
- `s` consists of lowercase English letters, uppercase English letters, and digits.

```
class Solution {
    public List<String> letterCasePermutation(String s) {
        List<String> res = new ArrayList<>();
        dfs(res, s, 0, new StringBuilder());
        return res;
    }
    public void dfs(List<String> res, String s, int index, StringBuilder sb){
        if(index > s.length() - 1){
            res.add(sb.toString());
            return;
        } 
        char c = s.charAt(index);
        if(!Character.isDigit(c)){//是字母
            dfs(res, s, index+1, sb.append(Character.toUpperCase(c)));
            sb.deleteCharAt(sb.length() - 1);
            dfs(res, s, index+1, sb.append(Character.toLowerCase(c)));
            sb.deleteCharAt(sb.length() - 1);
        }else{
            dfs(res, s, index+1, sb.append(c));
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```