# 241. Different Ways to Add Parentheses

Methods: Basic logic
Difficulty: Medium

Given a string `expression` of numbers and operators, return *all possible results from computing all the different possible ways to group numbers and operators*. You may return the answer in **any order**.

The test cases are generated such that the output values fit in a 32-bit integer and the number of different results does not exceed `104`.

**Example 1:**

```
Input: expression = "2-1-1"
Output: [0,2]
Explanation:
((2-1)-1) = 0
(2-(1-1)) = 2

```

**Example 2:**

```
Input: expression = "2*3-4*5"
Output: [-34,-14,-10,-10,10]
Explanation:
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10

```

**Constraints:**

- `1 <= expression.length <= 20`
- `expression` consists of digits and the operator `'+'`, `'-'`, and `'*'`.
- All the integer values in the input expression are in the range `[0, 99]`.

```java
class Solution {
    public List<Integer> diffWaysToCompute(String expression) {
        List<Integer> results = new ArrayList<>();

        for(int i = 0; i < expression.length(); i++){
            if(!Character.isDigit(expression.charAt(i))){//代表是符號,切成左右兩側
    
                List<Integer> left = diffWaysToCompute(expression.substring(0, i));
                List<Integer> right = diffWaysToCompute(expression.substring(i+1));
                //做計算!! 遍歷所有組合
                for(int l : left){
                    for(int r :right){
                        int val = perform(l, r, expression.charAt(i));
                        results.add(val);
                    }
                }
                //System.out.println(perform(left.get(0), right.get(0), expression.charAt(i)));
                //results.add(perform(left.get(0), right.get(0), expression.charAt(i)));
            }
            if(expression.length() == 1 && Character.isDigit(expression.charAt(i))){
                results.add(Character.getNumericValue(expression.charAt(i)));
            }
        }
				//純數字直接輸出
        if (results.size() == 0) {
            results.add(Integer.valueOf(expression));
        }
        return results;
    }
    // function to get the result of the operation
    public int perform(int x, int y, char op) {
        if(op == '+') return x + y;
        if(op == '-') return x - y;
        if(op == '*') return x * y;
        return 0;
    }
}
```