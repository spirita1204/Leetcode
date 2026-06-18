# 1344. Angle Between Hands of a Clock  

  Methods: Math </br> Difficulty: Medium </br> </br>Given two numbers, `hour` and `minutes`, return *the smaller angle (in degrees) formed between the *`hour`* and the *`minute`* hand*.

Answers within `10-5` of the actual value will be accepted as correct.

**Example 1:   **

![Image](https://assets.leetcode.com/uploads/2019/12/26/sample_1_1673.png)

```plain text
Input: hour = 12, minutes = 30
Output: 165
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2019/12/26/sample_2_1673.png)

```plain text
Input: hour = 3, minutes = 30
Output: 75
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2019/12/26/sample_3_1673.png)

```plain text
Input: hour = 3, minutes = 15
Output: 7.5   
```

**Constraints:**

- `1 <= hour <= 12`
- `0 <= minutes <= 59`
```java
class Solution {  
    public double angleClock(int hour, int minutes) {
        double x = hour + minutes / 60.0;
        double diff = (11.0 * x) % 12.0;// 相對速度
        return Math.min(diff, 12.0 - diff) * 30.0;
    }
}
```



