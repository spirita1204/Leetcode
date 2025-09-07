# 1304. Find N Unique Integers Sum up to Zero  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an integer `n`, return **any** array containing `n` **unique** integers such that they add up to `0`.

**Example 1:**

```plain text
Input: n = 5
Output: [-7,-1,1,3,4]
Explanation: These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].
```

**Example 2:**

```plain text
Input: n = 3
Output: [-1,0,1]
```

**Example 3:**

```plain text
Input: n = 1
Output: [0]
```

**Constraints:**

- `1 <= n <= 1000`
```java
class Solution {
    public int[] sumZero(int n) {
        int[] res = new int[n];

        if(n % 2 != 0) 
            for(int i = 0; i < n; i++) 
                res[i] = i - n/2;
        else 
            for(int i = 0; i < n; i++) {
                if(i < n / 2) 
                    res[i] = i - n/2;
                else 
                    res[i] = i - n/2 + 1;
            }
        return res;
    }
}
```

