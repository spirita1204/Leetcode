# 1550. Three Consecutive Odds  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an integer array arr, return true if there are three consecutive odd numbers in the array. Otherwise, return false

**Example 1:**

```plain text
Input: arr = [2,6,4,1]
Output: false
Explanation: There are no three consecutive odds.
```

**Example 2:**

```plain text
Input: arr = [1,2,34,3,4,5,7,23,12]
Output: true
Explanation: [5,7,23] are three consecutive odds.
```

**Constraints:**

- `1 <= arr.length <= 1000`
- `1 <= arr[i] <= 1000`
```java
class Solution {
    public boolean threeConsecutiveOdds(int[] arr) {
        int odds = 0;
        for(int i = 0; i < arr.length; i++) {
            if(arr[i] % 2 != 0) 
                odds++;
            else 
                odds = 0;
            if(odds == 3) return true;
        }
        return false;
    }
}
```

