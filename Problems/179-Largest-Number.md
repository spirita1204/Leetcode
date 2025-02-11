# 179. Largest Number

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Given a list of non-negative integers `nums`, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

**Example 1:**

```
Input: nums = [10,2]
Output: "210"

```

**Example 2:**

```
Input: nums = [3,30,34,5,9]
Output: "9534330"

```

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 109`

```java
class Solution {
    public String largestNumber(int[] nums) {
        // 56 5 -> 565 vs 556
        // 54 5 -> 554
        // 轉成字串比較
        StringBuilder sb = new StringBuilder();
        Integer[] numObjects = Arrays.stream(nums).boxed().toArray(Integer[]::new);
        // 按字典顺序排序
        Arrays.sort(numObjects,
                (a, b) -> (String.valueOf(b) + String.valueOf(a)).compareTo(String.valueOf(a) + String.valueOf(b)));
        // 将 Integer[] 转换回 int[]
        nums = Arrays.stream(numObjects).mapToInt(Integer::intValue).toArray();
        int cnt = 0;// 計算全部都是0情況
        for (int num : nums) {
            if(num == 0)
                cnt++;
            sb.append(num);
        }
        if(cnt == sb.length()) return "0";

        return sb.toString();

    }
}
```