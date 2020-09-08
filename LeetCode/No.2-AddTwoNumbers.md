## Description

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Thinking

1. 正常加减，满十进1，用 l1 储存结果数字，然后递归处理。时间复杂度O(n)，空间复杂度O(n)
2. 在1的基础上，使用循环而不使用递归

## Solutions

~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */

//Solutions 1
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) l1 = new ListNode(0);
        if (l2 == null) l2 = new ListNode(0);
        
        int sum = l1.val + l2.val;
        if (sum >= 10) {
            if (l1.next == null) l1.next = new ListNode(0);
            l1.next.val += 1;
            l1.val = sum - 10;
        } else {
            l1.val = sum;
        }
        if (l1.next == null && l2.next == null) return l1;
        l1.next = addTwoNumbers(l1.next, l2.next);
        return l1;
    }
}

// Solutions 2 from @potpie
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode c1 = l1;
        ListNode c2 = l2;
        ListNode sentinel = new ListNode(0);
        ListNode d = sentinel;
        int sum = 0;
        while (c1 != null || c2 != null) {
            sum /= 10;
            if (c1 != null) {
                sum += c1.val;
                c1 = c1.next;
            }
            if (c2 != null) {
                sum += c2.val;
                c2 = c2.next;
            }
            d.next = new ListNode(sum % 10);
            d = d.next;
        }
        if (sum / 10 == 1)
            d.next = new ListNode(1);
        return sentinel.next;
    }
}

// Solution 2 from me
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int sum = 0;
        ListNode result = new ListNode(0);
        ListNode p = result;
        while (l1 != null || l2 != null) {
            sum /= 10;
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            p.next = new ListNode(sum % 10);
            p = p.next;
        }
        if (sum / 10 == 1) {
            p.next = new ListNode(1);
            p = p.next;
        }
        return result.next;
    }
}
~~~



## Further

