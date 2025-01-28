# 1094. Car Pooling

Methods: Prefix Sum
Difficulty: Medium

```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        // O(ij)
        // int[] arr = new int[1000];
        // for(int i = 0; i < trips.length; i++) {
        //     int passengers  = trips[i][0];
        //     int from = trips[i][1];
        //     int to = trips[i][2];
        //     for(int j = from; j < to; j++) 
        //         arr[j] += passengers;
        // }
        // for(int i : arr) 
        //     if(i > capacity) return false;

        // return true;

        // O(n) prefix sum
        int[] prefix = new int[1001];
        //        1  3  5  7   
        // 0 0 0..2  3 -2 -3...
        for(int[] arr : trips){
			if(arr[0] > capacity) return false;
            prefix[arr[1]] += arr[0];// from
            prefix[arr[2]] -= arr[0];// to
        }
        
        for(int i = 1; i < prefix.length; i++){
            prefix[i] += prefix[i - 1];
            if(prefix[i] > capacity) return false;
        }

        return true;
    }
}
```