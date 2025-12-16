# 39. Combination Sum  

  Methods: DFS </br> Difficulty: Medium </br> </br>Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all ****unique combinations**** of *`candidates`* where the chosen numbers sum to *`target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the

frequency

of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/b5c271b2-2852-4452-ab56-cf17578a164a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TG63LY43%2F20251216%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20251216T113121Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCzfAzgO1Z9Jc76UI7Dj7IhCgv7aKz%2BlNs%2FCHq4f6hhIgIhAIapRMWxwyFLwttQDnOORE7HPZMRYiySOHmPsDtBK3wLKv8DCGQQABoMNjM3NDIzMTgzODA1IgxsYEQEJTdkEL8co2sq3APgUkcK8AoweY3VRO4JfaKHeA43Jt3XQ0hmTG%2FtgKYC%2BBO0RF2OtFk3P%2FDU79yYgJ%2FsXTn0%2FyN0m1SVESLhbsLcf0DuOfRwXPfRGPUw8Rj8LmwZTYSOwtM5LvHs4hnZHUQfUibv71%2BAVfrE%2FwROUahRdKGmdwaitag9fTpe43QLw9W8JTe0rTELdSOG5KK1m8uREytdOvgIWK0Iuv1T%2FtWP31QcA56E9lNk8FJzyGF4EbPN9sxZPsiPQPm0zVlL%2B813iPm3fiqyTLRSh%2Bee5y9GlsYiVhRn93Pr%2BJ6H9kV21e4G3RoTdZ34%2FGxRLQQjnkYF4ADBQhA%2BQLUWwTJqfFSL%2BYRbtbyhyPQn2prP5u9cVRsNvtQtAERytWt5zCmLnekR7JDqwq0vgkTBwDu5QaV4yjv%2FVaq05NCSL2tauO%2F%2Fp4AbHp51HzYmy8JXelSnjIxwWCIRWvZ5T%2FVHEB50oHLz0VZwaVMgnFCICTizNtXBPNdGqVemhc5HMh%2FnJ97GmAMZg8FVA5jjk5PgZDdgzJljDnt9jRyvW1dbuZJVyqF4YD1HNX3lhyCZusgDU5TuN8fj1%2Be5QygnTvPyXcppB7f0lOJu6ZfICBcJpiQuE78U%2FemuNKVJuBpLKYtU9jCI%2F4TKBjqkAbXfNeYOhx6m7vv1qY4T%2BHTjQLKFmxZgHE0EAgLJVa%2Fjgng%2BPkUtcPmU8G1q8XuKY1s2lK4niZmCrcrLsjbN03I2VbfsyMTvpBRVkj5BQRAL3P6HII2ZWUUk9bHw3WQz8fPaexAtuDQ0AZTuQBxfj0uoedARVJoAkfaYE2vx90%2FucPgvXdEhbR59qyA5KtzKBl%2FynESZemzLyMI2yVCh3pJq1PrL&X-Amz-Signature=db205decc065a7e74883948ebca4b390d0e41dfc0219dcb75db7bbbaefd3eb43&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Example 1:**

```plain text
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

```

**Example 2:**

```plain text
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]

```

**Example 3:**

```plain text
Input: candidates = [2], target = 1
Output: []
```

```java
class Solution {
    public  List<List<Integer>> combinationSum(int[] candidates, int target) {
		List<List<Integer>> resList = new ArrayList<>();
		List<Integer> subResList = new ArrayList<>();
		backtracking(candidates, 0, target, resList, subResList);
		return resList;
	}

	public  void backtracking(int[] candidates,int k , int target, List<List<Integer>> resList,
			List<Integer> subResList) { // 回朔法搜索recursion

		if (target == 0) {
			resList.add(new ArrayList<Integer>(subResList));//
			//錯 :resList.add(subResList);
			原因https://stackoverflow.com/questions/31064005/add-elements-to-listlistinteger
			return;
		}
		if (target < 0)
			return;
		for (int i = k; i < candidates.length; i++) {
			subResList.add(candidates[i]);
			backtracking(candidates, i, target - candidates[i], resList, subResList);
			subResList.remove(subResList.size() - 1);
		}

	}

}
```

