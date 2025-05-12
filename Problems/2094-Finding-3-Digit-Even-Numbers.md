# 2094. Finding 3-Digit Even Numbers  

  Methods: Basic logic </br> Data Structure: Hash Table </br> Difficulty: Easy </br> </br>You are given an integer array `digits`, where each element is a digit. The array may contain duplicates.

You need to find **all** the **unique** integers that follow the given requirements:

- The integer consists of the **concatenation** of **three** elements from `digits` in **any** arbitrary order.
- The integer does not have **leading zeros**.
- The integer is **even**.
For example, if the given `digits` were `[1, 2, 3]`, integers `132` and `312` follow the requirements.

Return *a ****sorted**** array of the unique integers.*

**Example 1:**

```plain text
Input: digits = [2,1,3,0]
Output: [102,120,130,132,210,230,302,310,312,320]
Explanation: All the possible integers that follow the requirements are in the output array.
Notice that there are noodd integers or integers withleading zeros.
```

**Example 2:**

```plain text
Input: digits = [2,2,8,8,2]
Output: [222,228,282,288,822,828,882]
Explanation: The same digit can be used as many times as it appears in digits.
In this example, the digit 8 is used twice each time in 288, 828, and 882.
```

**Example 3:**

```plain text
Input: digits = [3,7,5]
Output: []
Explanation: Noeven integers can be formed using the given digits.
```

**Constraints:**

- `3 <= digits.length <= 100`
- `0 <= digits[i] <= 9`
```java
class Solution {
    public int[] findEvenNumbers(int[] digits) {
        int[] map = new int[10];
        for (int i = 0; i < digits.length; i++) { // make a frequency map of digits
            map[digits[i]]++;
        }
        List<Integer> arr = new ArrayList<>();
        // 範圍100 ~ 999 判斷哪些可以組成
        for (int i = 100; i <= 999; i = i + 2) {
            int num = i;
            int[] freq = new int[10];
            while (num > 0) { // will always run 3 times
                int rem = num % 10;
                freq[rem]++;
                num = num / 10;
            }
            // 比較 是否足夠使用
            boolean isEnough = true;
            for (int j = 0; j < 10; j++) { // it will always run for at max 10 times
                if (freq[j] > map[j]) {
                    isEnough = false;
                    break;
                }
            }
            if (isEnough)
                arr.add(i);
        }
        int[] ans = new int[arr.size()]; // logic for arraylist to array conversion
        for (int i = 0; i < arr.size(); i++) { // at max we can have all num from 100 to 998 only
            ans[i] = arr.get(i);
        }

        return ans;
    }
}
```

