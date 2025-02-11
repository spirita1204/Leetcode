# 1346. Check If N and Its Double Exist

Methods: Binary Search
Data structure: Set
Difficulty: Easy

**Easy**

1.6K

172

Companies

Given an array `arr` of integers, check if there exist two indices `i` and `j` such that :

- `i != j`
- `0 <= i, j < arr.length`
- `arr[i] == 2 * arr[j]`

**Example 1:**

```
Input: arr = [10,2,5,3]
Output: true
Explanation: For i = 0 and j = 2, arr[i] == 10 == 2 * 5 == 2 * arr[j]

```

**Example 2:**

```
Input: arr = [3,1,7,11]
Output: false
Explanation: There is no i and j that satisfy the conditions.

```

**Constraints:**

- `2 <= arr.length <= 500`
- `103 <= arr[i] <= 103`

```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        Arrays.sort(arr);
        for(int i = 0; i< arr.length; i++){
            if(arr.length>= 2 && arr[i] == 0 && arr[i+1] == 0) return true;//特別處理0 0例外情況
            int left = 0;
            int right = arr.length - 1;
            while(left <= right){
                int mid = left + (right - left)/2;
                if(arr[mid] != arr[i] && arr[mid] == 2* arr[i]) return true;
                else if(arr[mid] < 2* arr[i]) left = mid + 1;
                else right = mid - 1;
            }
        }
        return false;
    }
    /** Set 更快
    public boolean checkIfExist(int[] arr) {
        HashSet<Integer> set = new HashSet<>();
        for(int a : arr) {
            if(set.contains(a*2) || (a%2 == 0 && set.contains(a/2))) return true;
            set.add(a);
        }
        return false;
    } */
}
```