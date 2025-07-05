# 1394. Find Lucky Integer in an Array  

  Methods: Sort </br> Difficulty: Easy </br> </br>Given an array of integers `arr`, a **lucky integer** is an integer that has a frequency in the array equal to its value.   

Return *the largest ****lucky integer**** in the array*. If there is no **lucky integer** return `-1`.

**Example 1:**

```plain text
Input: arr = [2,2,3,4]
Output: 2
Explanation: The only lucky number in the array is 2 because frequency[2] == 2.
```

**Example 2:**

```plain text
Input: arr = [1,2,2,3,3,3]
Output: 3
Explanation: 1, 2 and 3 are all lucky numbers, return the largest of them.
```

**Example 3:**

```plain text
Input: arr = [2,2,2,3,3]
Output: -1
Explanation: There are no lucky numbers in the array.
```

**Constraints:**

- `1 <= arr.length <= 500`
- `1 <= arr[i] <= 500`
```java
class Solution {
    public int findLucky(int[] arr) {
        Arrays.sort(arr);
        int len = arr.length;
        int pre = 0, cnt = 0;

        for(int i = len - 1; i >= 0; i--) {
            if(arr[i] == pre) 
                cnt++;
            else {
                pre = arr[i];
                cnt = 1;
            }
            if(i == 0 || arr[i - 1] != pre) {
                if(cnt == arr[i])
                    return cnt;
            }
        }
        return -1;
    }
}
```

