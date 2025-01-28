# 1552. Magnetic Force Between Two Balls

Methods: Binary Search
Difficulty: Medium

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/magnetic-force-between-two-balls/solutions/2996690/java-code-with-explanation/)

In the universe Earth C-137, Rick discovered a special form of magnetic force between two balls if they are put in his new invented basket. Rick has `n` empty baskets, the `ith` basket is at `position[i]`, Morty has `m` balls and needs to distribute the balls into the baskets such that the **minimum magnetic force** between any two balls is **maximum**.

Rick stated that magnetic force between two different balls at positions `x` and `y` is `|x - y|`.

Given the integer array `position` and the integer `m`. Return *the required force*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/08/11/q3v1.jpg](https://assets.leetcode.com/uploads/2020/08/11/q3v1.jpg)

```
Input: position = [1,2,3,4,7], m = 3
Output: 3
Explanation: Distributing the 3 balls into baskets 1, 4 and 7 will make the magnetic force between ball pairs [3, 3, 6]. The minimum magnetic force is 3. We cannot achieve a larger minimum magnetic force than 3.

```

**Example 2:**

```
Input: position = [5,4,3,2,1,1000000000], m = 2
Output: 999999999
Explanation: We can use baskets 1 and 1000000000.
```

```java
class Solution {
    public int maxDistance(int[] position, int m) {
        Arrays.sort(position);
        int left = 0;
        int right = (position[position.length-1]-position[0])/(m-1);//縮小搜索範圍 答案必定在這範圍當中 //切成m-1等分//

        while(left <= right){
            int mid = (left + right) / 2;
            if(isPossible(mid, m, position)){//可放小球 放大
                left = mid+1;
            }
            else{//不行放 縮小
                right = mid-1;
            }
        }
        return left - 1;
    }
    public boolean isPossible(int mid, int m, int[] position){//able to place all the balls with 'mid' as minimum distance.
        int b=1;
        int lastBall = position[0];
        for(int i = 1 ; i < position.length ; i++){
            if(position[i] - lastBall >= mid){
                b++;
                if(b == m)
                    return true;
                lastBall = position[i];                
            }   
        }
        return false; 
    }
}
```