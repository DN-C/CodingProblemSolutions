## Description

Given a string `s` and a character `c` that occurs in `s`, return *an array of integers `answer` where* `answer.length == s.length` *and* `answer[i]` *is the shortest distance from* `s[i]` *to the character* `c` *in* `s`.

 

**Example 1:**

```
Input: s = "loveleetcode", c = "e"
Output: [3,2,1,0,1,0,0,1,2,2,1,0]
```

**Example 2:**

```
Input: s = "aaab", c = "b"
Output: [3,2,1,0]
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s[i]` and `c` are lowercase English letters.
- `c` occurs at least once in `s`.

## Thinking

Record all positions of c first, then calculate distances.

Solution 2 comes from @lee215, a fantastic solution, completely out of my knowledge and imagination of algorithm. Details in Further part. Also a DP solution there.

## Solutions

~~~java
//Solution 1
class Solution {
    public int[] shortestToChar(String s, char c) {
        int len = s.length();
        int[] res = new int[len];
        ArrayList<Integer> record = new ArrayList<Integer>(); 
        for(int i = 0; i < len; i++) {
            if(s.charAt(i) == c) record.add(i);
        }
        int size = record.size();
        for(int i = record.get(0) - 1; i > -1; i--) res[i] = res[i + 1] + 1;
        for(int i = record.get(size - 1) + 1; i < len; i++) res[i] = res[i - 1] + 1;
        if(len > 1) {
            for(int i = 1; i < size; i++) {
                int left = record.get(i - 1), right = record.get(i), maxInBound = (left + right) / 2;
                while(left + 1 <= right - 1) {
                    res[left + 1] = res[left] + 1;
                    res[right - 1] = res[right] + 1;
                    left++; right--;
                }
            }
        }
        return res;
    }
}

//Solution 2
    public int[] shortestToChar(String S, char C) {
        int n = S.length(), pos = -n, res[] = new int[n];
        for (int i = 0; i < n; ++i) {
            if (S.charAt(i) == C) pos = i;
            res[i] = i - pos;
        }
        for (int i = pos - 1; i >= 0; --i) {
            if (S.charAt(i) == C)  pos = i;
            res[i] = Math.min(res[i], pos - i);
        }
        return res;
    }
~~~



## Further

https://leetcode.com/problems/shortest-distance-to-a-character/discuss/125788/C%2B%2BJavaPython-2-Pass-with-Explanation