# 941. Valid Mountain Array  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an array of integers `arr`, return `*true*`* if and only if it is a valid mountain array*.

Recall that arr is a mountain array if and only if:  

- `arr.length >= 3`
- There exists some `i` with `0 < i < arr.length - 1` such that:
![Image](https://assets.leetcode.com/uploads/2019/10/20/hint_valid_mountain_array.png)

**Example 1:**

```plain text
Input: arr = [2,1]
Output: false
```

**Example 2:**

```plain text
Input: arr = [3,5,5]
Output: false
```

**Example 3:**

```plain text
Input: arr = [0,3,2,1]
Output: true
```

**Constraints:**

- `1 <= arr.length <= 104`
- `0 <= arr[i] <= 104`
```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if(arr.length < 3) 
            return false;
        boolean up = true;

        for(int i = 1; i < arr.length; i++) {
            if(arr[i] == arr[i - 1])// not strict
                return false;
            if(arr[i] > arr[i - 1] && !up)// 非山峰
                return false;
            if(arr[i] < arr[i - 1]) {// 轉向
                if(i < 2)// 至少要有上升
                    return false;
                up = false;
            }
        }
        
        return (up) ? false : true;
    }
}
```

