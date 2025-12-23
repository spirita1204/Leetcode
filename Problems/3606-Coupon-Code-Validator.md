# 3606. Coupon Code Validator  

  Data Structure: Hash Table </br> Difficulty: Easy </br> </br>You are given three arrays of length `n` that describe the  properties of `n` coupons: `code`, `businessLine`, and `isActive`. The `ith `coupon has:

- `code[i]`: a **string** representing the coupon identifier.
- `businessLine[i]`: a **string** denoting the business category of the coupon.
- `isActive[i]`: a **boolean** indicating whether the coupon is currently active.
A coupon is considered **valid** if all of the following conditions hold:

1. `code[i]` is non-empty and consists only of alphanumeric characters (a-z, A-Z, 0-9) and underscores (`_`).
1. `businessLine[i]` is one of the following four categories: `"electronics"`, `"grocery"`, `"pharmacy"`, `"restaurant"`.
1. `isActive[i]` is **true**.
Return an array of the **codes** of all valid coupons, **sorted** first by their **businessLine** in the order: `"electronics"`, `"grocery"`, `"pharmacy", "restaurant"`, and then by **code** in lexicographical (ascending) order within each category.

**Example 1:**

**Input:** code = ["SAVE20","","PHARMA5","SAVE@20"], businessLine = ["restaurant","grocery","pharmacy","restaurant"], isActive = [true,true,true,true]

**Output:** ["PHARMA5","SAVE20"]

**Explanation:**

- First coupon is valid.
- Second coupon has empty code (invalid).
- Third coupon is valid.
- Fourth coupon has special character `@` (invalid).
**Example 2:**

**Input:** code = ["GROCERY15","ELECTRONICS_50","DISCOUNT10"], businessLine = ["grocery","electronics","invalid"], isActive = [false,true,true]

**Output:** ["ELECTRONICS_50"]

**Explanation:**

- First coupon is inactive (invalid).
- Second coupon is valid.
- Third coupon has invalid business line (invalid).
**Constraints:**

- `n == code.length == businessLine.length == isActive.length`
- `1 <= n <= 100`
- `0 <= code[i].length, businessLine[i].length <= 100`
- `code[i]` and `businessLine[i]` consist of printable ASCII characters.
- `isActive[i]` is either `true` or `false`.
```java
class Solution {
    public List<String> validateCoupons(String[] code, String[] businessLine, boolean[] isActive) {
        List<String> res = new ArrayList();

        List<String> e = new ArrayList();
        List<String> g = new ArrayList();
        List<String> p = new ArrayList();
        List<String> r = new ArrayList();

        for (int i = 0; i < isActive.length; i++) {
            if (!isActive[i])
                continue;
            if (!(businessLine[i].equals("electronics")
                    || businessLine[i].equals("grocery")
                    || businessLine[i].equals("pharmacy")
                    || businessLine[i].equals("restaurant")))
                continue;
            if (code[i].length() == 0)
                continue;
            boolean found = true;
            for (int j = 0; j < code[i].length(); j++) {
                char ch = code[i].charAt(j);
                if (!Character.isLetterOrDigit(ch) && ch != '_') {
                    found = false;
                    break;
                }
            }

            if (found) {
                if (businessLine[i].startsWith("e"))
                    e.add(code[i]);
                if (businessLine[i].startsWith("g"))
                    g.add(code[i]);
                if (businessLine[i].startsWith("p"))
                    p.add(code[i]);
                if (businessLine[i].startsWith("r"))
                    r.add(code[i]);
            }

        }
        Collections.sort(e);
        Collections.sort(g);
        Collections.sort(p);
        Collections.sort(r);
        res.addAll(e);
        res.addAll(g);
        res.addAll(p);
        res.addAll(r);

        return res;
    }
}
```

