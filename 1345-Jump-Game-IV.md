# 1345. Jump Game IV

Methods: BFS
Data structure: Set
Difficulty: Hard

Given an array of integers `arr`, you are initially positioned at the first index of the array.

In one step you can jump from index `i` to index:

- `i + 1` where: `i + 1 < arr.length`.
- `i - 1` where: `i - 1 >= 0`.
- `j` where: `arr[i] == arr[j]` and `i != j`.

Return *the minimum number of steps* to reach the **last index** of the array.

Notice that you can not jump outside of the array at any time.

**Example 1:**

```
Input: arr = [100,-23,-23,404,100,23,23,23,3,404]
Output: 3
Explanation: You need three jumps from index 0 --> 4 --> 3 --> 9. Note that index 9 is the last index of the array.

```

**Example 2:**

```
Input: arr = [7]
Output: 0
Explanation: Start index is the last index. You do not need to jump.

```

**Example 3:**

```
Input: arr = [7,6,9,6,9,6,9,7]
Output: 1
Explanation: You can jump directly from index 0 to index 7 which is last index of the array.

```

**Constraints:**

- `1 <= arr.length <= 5 * 104`
- `108 <= arr[i] <= 108`

```java
class Solution {
    public int minJumps(int[] arr) {
        // i + 1
        // i - 1
        // arr[i] = arr[j]
        Map<Integer,Set<Integer>> hm = new HashMap<>();
        for(int i = 0 ; i < arr.length ; i++){
            if(!hm.containsKey(arr[i])){ 
                hm.put(arr[i], new HashSet<Integer>()); 
            }
            hm.get(arr[i]).add(i);
        }
        Queue<Integer> q = new ArrayDeque<>();
        q.offer(0);
        int[] visited = new int[arr.length];
        visited[0] = 1;
        int step = 0;

        while(!q.isEmpty()){
            int size = q.size();//定義當前同一波數量
            while(size-- > 0){//掃過同一階層
                int pos = q.poll();
                if(pos == arr.length - 1) return step;    
                if(pos + 1 < arr.length && visited[pos + 1]++ < 1){//超出邊界
                    q.offer(pos + 1);
                }   
                if(pos - 1 >= 0 && visited[pos - 1]++ < 1){//超出邊界
                    q.offer(pos - 1);
                }     
                for(int newPos : hm.get(arr[pos])){
                    // Consider example: [1,1,1,1,1,1,.....(5000 terms), 11] -> Answer =2;
                    //[7,7,2,1,7,7,7,3,4,1]上下有邊界端點要保留
                    if(newPos < arr.length && newPos >= 0 && visited[newPos]++ < 1){//超出邊界
                        q.offer(newPos);
                    }
                }
                //刪掉不再用的  不做會TLE!!
                hm.get(arr[pos]).clear();
            }
            step++;
        }
        return 0;
    }
}
```