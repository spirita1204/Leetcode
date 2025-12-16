# 494. Target Sum  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.
Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

```plain text
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3

```

**Example 2:**

```plain text
Input: nums = [1], target = 1
Output: 1

```

**Constraints:**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `1000 <= target <= 1000`
DFS

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        return dfs(nums, target, 0, 0);
    }
    public int dfs(int[] nums, int target, int pointer, int sum){
        if(pointer >= nums.length && sum == target) return 1;  
        if(pointer >= nums.length && sum != target) return 0;

        int addCount = dfs(nums, target, pointer + 1, sum + nums[pointer]);
        int subCount = dfs(nums, target, pointer + 1, sum - nums[pointer]);

        return addCount + subCount;
    }
}
```

DP最優解 

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/557222bb-d6e0-4278-a1d5-2cf6f1374f85/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q2RCTJN3%2F20251216%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20251216T113131Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGOfkSPP8v4ecd9YDc2IIY%2BqP9Fp6sixN4KbWzbkJDmAIgKwN%2F73dYjZ8ALTQjm9PYk8kddxc0ZXvOkvoLeIdMxOEq%2FwMIZBAAGgw2Mzc0MjMxODM4MDUiDAvhcL7eqlIFKkZacCrcAw7XEmULwqfJTMNIG8bAoYwO8zMIsCtb3dqgZfvP9lOBOZDGJPItHLyeDXw%2Bg%2BXQdulzYQlTnt575k4w1xYLxwWoKBvztjCZIExBmc5pzqJ%2F7b9H8vTzPrXJNCAXwnQE4EZ4iNpyJNkb9H%2F2U1MccFeQW73n9CsfauNN%2BRZKGAHbtfO8QjyMlzvcUMbiNWoWnFPlpJyA9dRja%2F3WLp5WYZ34EEIrcb%2BoXSQ%2BaIJOcjSbM%2FEDa8wam8umXNFnHmxBulK24Yca6mZUmtNBB5MVE7gT587AH92mAfAd7buCdg5MGbVLluG5KPi4vFKbIImqtYK6Bg%2FvoEAzyHSHzVVMxQWInBCj349ikPmGYHpQVro%2FVh4UDsB6slfoR08NeOLw0XLgPy4lCVe6bgYAVe%2FlG5cy3Z4kH95r1zuvN96pnBfMCafw8TVXu0x7vda2WbpQQFm8UQexVC%2BXEf0FQsjNBcR696MXyvEDitXbc4DEONom4enYrgzVjq6%2B2B6%2B%2Fu8VkXmi8HFoAd8TGaRHhyCUMducvNzTsCYbdBtbmldJtWNfhOpk0BRddw5jFczlFlPdZoBqV2hI6ATU2cq%2B5ONcWit%2F4ejVwXNkafrHfH%2BQzNHrzMG%2Fa65ki%2BCguSP0MKH%2FhMoGOqUBtuw4Q4BhbHrbI8MnwpzI9tMQTG2T%2FKK4x5Cy5A1y6h9szlgptqnyI4Gw4pws%2F31Emlw5AFKQOQkNYe%2F9ZX5Qzk75BWGWDjzjvoqmGpQjc%2FaQKgIqmurgt9CnoNzieCE4aWhxiFQ70fJ2suZF6ubH4GM9ev9NA7Nbyf4Dol%2BSsB6QkZb4Gzs4%2FjcZl6CUoAYUgXUxm3l4n1mLEggm8U12fe0%2FvJYO&X-Amz-Signature=412b77037b8062e282a7dc9ea87d2c4be7154b0809be20e1bb914621667de6a8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/751f9c95-51ff-4756-9689-bc5002142434/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q2RCTJN3%2F20251216%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20251216T113131Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGOfkSPP8v4ecd9YDc2IIY%2BqP9Fp6sixN4KbWzbkJDmAIgKwN%2F73dYjZ8ALTQjm9PYk8kddxc0ZXvOkvoLeIdMxOEq%2FwMIZBAAGgw2Mzc0MjMxODM4MDUiDAvhcL7eqlIFKkZacCrcAw7XEmULwqfJTMNIG8bAoYwO8zMIsCtb3dqgZfvP9lOBOZDGJPItHLyeDXw%2Bg%2BXQdulzYQlTnt575k4w1xYLxwWoKBvztjCZIExBmc5pzqJ%2F7b9H8vTzPrXJNCAXwnQE4EZ4iNpyJNkb9H%2F2U1MccFeQW73n9CsfauNN%2BRZKGAHbtfO8QjyMlzvcUMbiNWoWnFPlpJyA9dRja%2F3WLp5WYZ34EEIrcb%2BoXSQ%2BaIJOcjSbM%2FEDa8wam8umXNFnHmxBulK24Yca6mZUmtNBB5MVE7gT587AH92mAfAd7buCdg5MGbVLluG5KPi4vFKbIImqtYK6Bg%2FvoEAzyHSHzVVMxQWInBCj349ikPmGYHpQVro%2FVh4UDsB6slfoR08NeOLw0XLgPy4lCVe6bgYAVe%2FlG5cy3Z4kH95r1zuvN96pnBfMCafw8TVXu0x7vda2WbpQQFm8UQexVC%2BXEf0FQsjNBcR696MXyvEDitXbc4DEONom4enYrgzVjq6%2B2B6%2B%2Fu8VkXmi8HFoAd8TGaRHhyCUMducvNzTsCYbdBtbmldJtWNfhOpk0BRddw5jFczlFlPdZoBqV2hI6ATU2cq%2B5ONcWit%2F4ejVwXNkafrHfH%2BQzNHrzMG%2Fa65ki%2BCguSP0MKH%2FhMoGOqUBtuw4Q4BhbHrbI8MnwpzI9tMQTG2T%2FKK4x5Cy5A1y6h9szlgptqnyI4Gw4pws%2F31Emlw5AFKQOQkNYe%2F9ZX5Qzk75BWGWDjzjvoqmGpQjc%2FaQKgIqmurgt9CnoNzieCE4aWhxiFQ70fJ2suZF6ubH4GM9ev9NA7Nbyf4Dol%2BSsB6QkZb4Gzs4%2FjcZl6CUoAYUgXUxm3l4n1mLEggm8U12fe0%2FvJYO&X-Amz-Signature=e482cfa34c27cf706432bb725955ba7ff63b05fabda67b76fb50e550a218a94a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/3ecab7e9-6526-4896-8f2e-b31b3526f402/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q2RCTJN3%2F20251216%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20251216T113131Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGOfkSPP8v4ecd9YDc2IIY%2BqP9Fp6sixN4KbWzbkJDmAIgKwN%2F73dYjZ8ALTQjm9PYk8kddxc0ZXvOkvoLeIdMxOEq%2FwMIZBAAGgw2Mzc0MjMxODM4MDUiDAvhcL7eqlIFKkZacCrcAw7XEmULwqfJTMNIG8bAoYwO8zMIsCtb3dqgZfvP9lOBOZDGJPItHLyeDXw%2Bg%2BXQdulzYQlTnt575k4w1xYLxwWoKBvztjCZIExBmc5pzqJ%2F7b9H8vTzPrXJNCAXwnQE4EZ4iNpyJNkb9H%2F2U1MccFeQW73n9CsfauNN%2BRZKGAHbtfO8QjyMlzvcUMbiNWoWnFPlpJyA9dRja%2F3WLp5WYZ34EEIrcb%2BoXSQ%2BaIJOcjSbM%2FEDa8wam8umXNFnHmxBulK24Yca6mZUmtNBB5MVE7gT587AH92mAfAd7buCdg5MGbVLluG5KPi4vFKbIImqtYK6Bg%2FvoEAzyHSHzVVMxQWInBCj349ikPmGYHpQVro%2FVh4UDsB6slfoR08NeOLw0XLgPy4lCVe6bgYAVe%2FlG5cy3Z4kH95r1zuvN96pnBfMCafw8TVXu0x7vda2WbpQQFm8UQexVC%2BXEf0FQsjNBcR696MXyvEDitXbc4DEONom4enYrgzVjq6%2B2B6%2B%2Fu8VkXmi8HFoAd8TGaRHhyCUMducvNzTsCYbdBtbmldJtWNfhOpk0BRddw5jFczlFlPdZoBqV2hI6ATU2cq%2B5ONcWit%2F4ejVwXNkafrHfH%2BQzNHrzMG%2Fa65ki%2BCguSP0MKH%2FhMoGOqUBtuw4Q4BhbHrbI8MnwpzI9tMQTG2T%2FKK4x5Cy5A1y6h9szlgptqnyI4Gw4pws%2F31Emlw5AFKQOQkNYe%2F9ZX5Qzk75BWGWDjzjvoqmGpQjc%2FaQKgIqmurgt9CnoNzieCE4aWhxiFQ70fJ2suZF6ubH4GM9ev9NA7Nbyf4Dol%2BSsB6QkZb4Gzs4%2FjcZl6CUoAYUgXUxm3l4n1mLEggm8U12fe0%2FvJYO&X-Amz-Signature=f09fc207325d53780d80fef116bfedb4d6679f70840347ceb76d2ba03734b2a6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        return dp(nums, target);
    }
    public int dp(int[] nums, int target){//ways[i][j] # of ways to sum up to j using nums[0~i] 
        //             = ways[i - 1][j - nums[i]] + ways[i - 1][j - nums[i]]
        //init : ways[-1][0] = 1 無任何樹構成0 是ok的
        //ans : ways[m - 1][s]
        int sum = 0;
        for(int i : nums){
            sum += i;
        }
        int ways[][] = new int[nums.length + 1][sum*2+1];
        ways[0][sum] = 1;
        for(int i = 1; i <= nums.length; i++){
            for(int j = 0; j < sum*2+1; j++){
                if(j - nums[i - 1] < 0) ways[i][j] = ways[i - 1][j + nums[i - 1]];
                else if(j + nums[i - 1]  > sum*2) ways[i][j] = ways[i - 1][j - nums[i - 1]];
                else ways[i][j] = ways[i - 1][j - nums[i - 1]] + ways[i - 1][j + nums[i - 1]];
            }
        }
        return (target > sum || target < -sum) ? 0 : ways[nums.length][sum+target];
    }
}
```

