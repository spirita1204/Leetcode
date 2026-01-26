# 1200. Minimum Absolute Difference  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an array of distinct integers arr, find all pairs of elements with the minimum absolute difference of any two elements.

Return a list of pairs in ascending order(with respect to pairs), each pair [a, b] follows

- a, b are from arr.      
- a < b
- b - a equals to the minimum absolute difference of any two elements in arr
Example 1:

```plain text
Input: arr = [4,2,1,3]
Output: [[1,2],[2,3],[3,4]]
Explanation:The minimum absolute difference is 1. List all pairs with difference equal to 1 in ascending order.
```

**Example 2:**

```plain text
Input: arr = [1,3,6,10,15]
Output: [[1,3]]
```

**Example 3:   **

```plain text
Input: arr = [3,8,-10,23,19,-4,-14,27]
Output: [[-14,-10],[19,23],[23,27]]
```

**Constraints:**

- `2 <= arr.length <= 105`
- `106 <= arr[i] <= 106`
```java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(arr);
        int min = Integer.MAX_VALUE;
        for(int i = 1; i < arr.length; i++) {
            int now = arr[i] - arr[i - 1];
            if(now < min) {
                min = now;
                res.clear();
                res.add(Arrays.asList(arr[i - 1], arr[i]));
            } else if(now == min) {
                res.add(Arrays.asList(arr[i - 1], arr[i]));
            }
        }  
 
        return res;
    }
}
```

