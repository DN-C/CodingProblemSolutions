## Description

Given a balanced parentheses string `S`, compute the score of the string based on the following rule:

- `()` has score 1
- `AB` has score `A + B`, where A and B are balanced parentheses strings.
- `(A)` has score `2 * A`, where A is a balanced parentheses string.

 

**Example 1:**

```
Input: "()"
Output: 1
```

**Example 2:**

```
Input: "(())"
Output: 2
```

**Example 3:**

```
Input: "()()"
Output: 2
```

**Example 4:**

```
Input: "(()(()))"
Output: 6
```

 

**Note:**

1. `S` is a balanced parentheses string, containing only `(` and `)`.
2. `2 <= S.length <= 50`

## Thinking

Stack

Also an array solution and an O(1) space solution in [Further](#Further).

## Solutions

~~~java
class Solution {
    public int scoreOfParentheses(String S) {
        Stack<Integer> stack = new Stack<Integer>();
        int res = 0;
        for(char c : S.toCharArray()) {
            if(c == '(') {
                stack.push((int)c);
            } else if(c == ')') {
                int sum = 0;
                while(stack.peek() != '(') {
                    sum += stack.pop();
                }
                stack.pop();
                stack.push(sum == 0 ? 100 : 2 * sum);
            }
        }
        while(!stack.empty()) {
            res += stack.pop();
        }
        return res / 100;
    }
}
~~~



## Further

https://leetcode.com/problems/score-of-parentheses/discuss/141777/C%2B%2BJavaPython-O(1)-Space