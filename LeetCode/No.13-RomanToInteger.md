## Description

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

 

**Example 1:**

```
Input: s = "III"
Output: 3
```

**Example 2:**

```
Input: s = "IV"
Output: 4
```

**Example 3:**

```
Input: s = "IX"
Output: 9
```

**Example 4:**

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 5:**

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

 

**Constraints:**

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

## Thinking

Iterate in reverse order, add corresponding number when meet 'V', 'L', 'D', 'M', add or subtract corresponding number when meet 'I', 'X', 'C' determined by sum of previous numbers is larger than 5, 50, 500 or not. 

This idea is fully credited to @makeitture in comment section of Link in [Further](#Further). The intuitive idea came to my mind was adding in regular order, when meet 'I', 'X', 'C', check if the next character is 'V', 'L', 'D', 'M', then add different numbers and move two steps. 

## Solutions

~~~java
class Solution {
    public int romanToInt(String s) {
        int len = s.length(), res = 0;
        for(int i = len - 1; i >= 0; --i) {
            switch(s.charAt(i)) {
                case 'I':
                    res += res >= 5 ? -1 : 1;
                    break;
                case 'V':
                    res += 5;
                    break;
                case 'X':
                    res += res >= 50 ? -10 : 10;
                    break;
                case 'L':
                    res += 50;
                    break;
                case 'C':
                    res += res >= 500 ? -100 : 100;
                    break;
                case 'D':
                    res += 500;
                    break;
                case 'M':
                    res += 1000;
                    break;
            }
        }
        return res; 
    }
}
~~~



## Further

[Link](https://leetcode.com/problems/roman-to-integer/discuss/6529/My-solution-for-this-question-but-I-don't-know-is-there-any-easier-way)