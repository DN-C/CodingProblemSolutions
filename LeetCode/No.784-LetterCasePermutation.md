## Description

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.

Return *a list of all possible strings we could create*. You can return the output in **any order**.

 

**Example 1:**

```
Input: S = "a1b2"
Output: ["a1b2","a1B2","A1b2","A1B2"]
```

**Example 2:**

```
Input: S = "3z4"
Output: ["3z4","3Z4"]
```

**Example 3:**

```
Input: S = "12345"
Output: ["12345"]
```

**Example 4:**

```
Input: S = "0"
Output: ["0"]
```

 

**Constraints:**

- `S` will be a string with length between `1` and `12`.
- `S` will consist only of letters or digits.

## Thinking

Recursion(Actually DFS)

BFS in [Further](#Further)

## Solutions

~~~java
class Solution {
    public List<String> letterCasePermutation(String S) {
        ArrayList<String> res = new ArrayList<String>();
        divide(res, S.toCharArray(), 0, new String());
        return res;
    }
    
    public void divide(ArrayList<String> res, char[] s, int index, String str) {
        if(index > s.length) {
            return;   
        } else if(index == s.length) {
            res.add(str);
            return;
        }
        char c = s[index];
        if(c <= '9') {
            String newStr = new String(str);
            divide(res, s, index + 1, newStr + c);
        } else if(c <= 'Z') {
            String newStr1 = new String(str), newStr2 = new String(str);
            divide(res, s, index + 1, newStr1 + c);
            divide(res, s, index + 1, newStr2 + (char)(c + 32));
        } else if(c <= 'z') {
            String newStr1 = new String(str), newStr2 = new String(str);
            divide(res, s, index + 1, newStr1 + c);
            divide(res, s, index + 1, newStr2 + (char)(c - 32));
        }
    }
}
~~~



## Further

https://leetcode.com/problems/letter-case-permutation/discuss/115485/Java-Easy-BFS-DFS-solution-with-explanation