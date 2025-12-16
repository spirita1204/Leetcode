# 1291. Sequential Digits  

  Data Structure: Queue </br> Difficulty: Medium </br> </br>Medium

An integer has *sequential digits* if and only if each digit in the number is one more than the previous digit.

Return a **sorted** list of all the integers in the range `[low, high]` inclusive that have sequential digits.

**Example 1:**

```plain text
Input: low = 100, high = 300
Output: [123,234]

```

**Example 2:**

```plain text
Input: low = 1000, high = 13000
Output: [1234,2345,3456,4567,5678,6789,12345]

```

**Constraints:**

- `10 <= low <= high <= 10^9`
```java
class Solution {
    public List<Integer> sequentialDigits(int low, int high) {
        List<Integer> res = new ArrayList<>();

        // 先定義 Queue儲存1, 2, 3, 4, 5, 6, 7, 8, 9
        Queue<Integer> q = new ArrayDeque<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9));

        // 依次推出資料 並推入新資料
        while(!q.isEmpty()) {
            int num = q.poll(); // 取出最前

            if(num > high) return res;
            if(low <= num && num <= high) res.add(num);
            // 塞入新連續資料234
            int r = num % 10;
            if(r != 9) q.offer(num * 10 + r + 1);// 避免易位
        }

        return res;
    }
}
```

