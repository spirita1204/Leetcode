# 118. Pascal's Triangle

Methods: Basic logic
Difficulty: Easy

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

```

**Example 2:**

```
Input: numRows = 1
Output: [[1]]

```

**Constraints:**

- `1 <= numRows <= 30`

```jsx
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<>();
        recursion(1, numRows, res);
        return res;
    }
    public void recursion(int count, int numRows, List<List<Integer>> res){
        List<Integer> sub = new ArrayList<>();
        if(count == 1){
            sub.add(1);
            res.add(new ArrayList<Integer>(sub));
            recursion(count + 1, numRows, res);
        }else if(count <= numRows){
            sub.add(1);
            for(int i = 1; i < res.get(count - 2).size(); i++){
                int fir = res.get(count - 2).get(i - 1);
                int sec = res.get(count - 2).get(i);
                sub.add(fir + sec);
            }
            sub.add(1);
            res.add(sub);
            recursion(count + 1, numRows, res);
        }
    }
}
```