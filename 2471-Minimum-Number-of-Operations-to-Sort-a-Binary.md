# 2471. Minimum Number of Operations to Sort a Binary Tree by Level

Methods: BFS
Difficulty: Medium++

You are given the `root` of a binary tree with **unique values**.

In one operation, you can choose any two nodes **at the same level** and swap their values.

Return *the minimum number of operations needed to make the values at each level sorted in a **strictly increasing order***.

The **level** of a node is the number of edges along the path between it and the root node*.*

**Example 1:**

![https://assets.leetcode.com/uploads/2022/09/18/image-20220918174006-2.png](https://assets.leetcode.com/uploads/2022/09/18/image-20220918174006-2.png)

```
Input: root = [1,4,3,7,6,8,5,null,null,null,null,9,null,10]
Output: 3
Explanation:
- Swap 4 and 3. The 2nd level becomes [3,4].
- Swap 7 and 5. The 3rd level becomes [5,6,8,7].
- Swap 8 and 7. The 3rd level becomes [5,6,7,8].
We used 3 operations so return 3.
It can be proven that 3 is the minimum number of operations needed.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/09/18/image-20220918174026-3.png](https://assets.leetcode.com/uploads/2022/09/18/image-20220918174026-3.png)

```
Input: root = [1,3,2,7,6,5,4]
Output: 3
Explanation:
- Swap 3 and 2. The 2nd level becomes [2,3].
- Swap 7 and 4. The 3rd level becomes [4,6,5,7].
- Swap 6 and 5. The 3rd level becomes [4,5,6,7].
We used 3 operations so return 3.
It can be proven that 3 is the minimum number of operations needed.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2022/09/18/image-20220918174052-4.png](https://assets.leetcode.com/uploads/2022/09/18/image-20220918174052-4.png)

```
Input: root = [1,2,3,4,5,6]
Output: 0
Explanation: Each level is already sorted in increasing order so return 0.

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `1 <= Node.val <= 105`
- All the values of the tree are **unique**.

---

Seen this question in a real interview before?

**1/5**

Yes

No

Accepted

**73.9K**

Submissions

**101.9K**

Acceptance Rate

**72.5%**

---

Topics

---

Companies

---

Hint 1

We can group the values level by level and solve each group independently.

---

Hint 2

Do BFS to group the value level by level.

---

Hint 3

Find the minimum number of swaps to sort the array of each level.

---

Hint 4

While iterating over the array, check the current element, and if not in the correct index, replace that element with the index of the element which should have come.

```java
class Solution {
    public int minimumOperations(TreeNode root) {
        Queue<TreeNode> pq = new LinkedList<>();
        pq.offer(root);
        int res = 0;
        
        while (!pq.isEmpty()) {
            int size = pq.size();
            List<Integer> arr = new ArrayList<>();
            
            while (size-- > 0) {
                TreeNode e = pq.poll();
                if (e.left != null) {
                    pq.offer(e.left);
                    arr.add(e.left.val);
                }
                if (e.right != null) {
                    pq.offer(e.right);
                    arr.add(e.right.val);   
                }
            }
            
            if (!arr.isEmpty()) {
                res += minSwapsToSort(arr);
            }
        }
        
        return res;
    }
    
    private int minSwapsToSort(List<Integer> arr) {
        int n = arr.size();
        int[] sortedArr = arr.stream().sorted().mapToInt(i -> i).toArray();
        Map<Integer, Integer> indexMap = new HashMap<>();
        
        for (int i = 0; i < n; i++) {
            indexMap.put(arr.get(i), i);
        }
        
        boolean[] visited = new boolean[n];
        int swaps = 0;
        
        for (int i = 0; i < n; i++) {
            if (visited[i] || sortedArr[i] == arr.get(i)) {
                continue;
            }
            
            int cycleSize = 0;
            int x = i;
            
            while (!visited[x]) {
                visited[x] = true;
                x = indexMap.get(sortedArr[x]);
                cycleSize++;
            }
            
            if (cycleSize > 1) {
                swaps += (cycleSize - 1);
            }
        }
        
        return swaps;
    }
}

```