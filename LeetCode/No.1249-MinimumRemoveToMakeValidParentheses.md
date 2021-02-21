## Description

Given a string s of `'('` , `')'` and lowercase English characters. 

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

 

**Example 1:**

```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```

**Example 2:**

```
Input: s = "a)b(c)d"
Output: "ab(c)d"
```

**Example 3:**

```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.
```

**Example 4:**

```
Input: s = "(a(b(c)d)"
Output: "a(b(c)d)"
```

 

**Constraints:**

- `1 <= s.length <= 10^5`
- `s[i]` is one of `'('` , `')'` and lowercase English letters`.`

## Thinking

Loop twice, one in regular order and other in reverse order. First time we delete all unnecessary ')', the second time '('.

Use StringBuffer to reduce space usage.

An optimized solution in the first link of [Further](#Further), and another stack solution in the second link.

## Solutions

~~~java
class Solution {
    public String minRemoveToMakeValid(String s) {
        if(s.length() == 1) return s; 
        StringBuffer strbuf = new StringBuffer(s);
        int num = 0;
        for(int i = 0, len = strbuf.length(); i < len; i++) {
            char c = strbuf.charAt(i);
            if(c == '(') ++num;
            if(c == ')') --num;
            if(num < 0) {
                ++num;
                strbuf.deleteCharAt(i);
                len = strbuf.length();
                i--;
            }
        }
        num = 0;
        for(int i = strbuf.length() - 1; i >= 0; i--) {
            char c = strbuf.charAt(i);
            if(c == ')') ++num;
            if(c == '(') --num;
            if(num < 0) {
                ++num;
                strbuf.deleteCharAt(i);
            }
        }
        return strbuf.toString();
    }
}
~~~



## Further

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/discuss/419443/Java-Clean-StringBuilder-solution

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/discuss/419402/JavaC%2B%2B-Stack