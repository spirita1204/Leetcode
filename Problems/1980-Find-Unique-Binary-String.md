# 1980. Find Unique Binary String  

  Methods: DFS </br> Difficulty: Medium </br> </br>Given an array of strings `nums` containing `n` **unique** binary strings each of length `n`, return *a binary string of length *`n`* that ****does not appear**** in *`nums`*. If there are multiple answers, you may return ****any**** of them*.

**Example 1:**

```plain text
Input: nums = ["01","10"]
Output: "11"
Explanation: "11" does not appear in nums. "00" would also be correct.
```

**Example 2:**

```plain text
Input: nums = ["00","01"]
Output: "11"
Explanation: "11" does not appear in nums. "10" would also be correct.
```

**Example 3:**

```plain text
Input: nums = ["111","011","001"]
Output: "101"
Explanation: "101" does not appear in nums. "000", "010", "100", and "110" would also be correct.
```

**Constraints:**

- `n == nums.length`
- `1 <= n <= 16`
- `nums[i].length == n`
- `nums[i] `is either `'0'` or `'1'`.
- All the strings of `nums` are **unique**.
### DFS

```java
class Solution {
    String res;

    public String findDifferentBinaryString(String[] nums) {
        int len = nums.length;
        List<String> numsList = Arrays.asList(nums);

        dfs(numsList, 0, len, new StringBuilder());

        return res;
    }

    private void dfs(List<String> numsList, int n, int len, StringBuilder sb) {
        if(n == len) {
            if(!numsList.contains(sb.toString())) {
                res = sb.toString();
                return;
            } else {
                return;
            }
        }
        sb.append(1);
        dfs(numsList, n + 1, len, sb);
        sb.deleteCharAt(sb.length() - 1);

        sb.append(0);
        dfs(numsList, n + 1, len, sb);
        sb.deleteCharAt(sb.length() - 1);
    }
}
```

### String

```javascript
class Solution {
    public String findDifferentBinaryString(String[] nums) {
        StringBuilder ans = new StringBuilder();
        for (int i=0;i<nums.length;i++){
            ans.append(nums[i].charAt(i) == '0' ? '1' :'0');
        }
        return ans.toString();
    }
}
```



