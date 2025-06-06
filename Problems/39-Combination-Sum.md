# 39. Combination Sum

Methods: DFS
Difficulty: Medium

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the

frequency

of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

![Untitled](Untitled.png)

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]

```

**Example 3:**

```
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