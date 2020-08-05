## Description

06-PrintLinkedListReverse

## Thinking

递归or栈

取巧可以用Collection.reverse()



## Solutions

~~~java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.*;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ListNode Node = listNode;
        ArrayList<Integer> list = new ArrayList<Integer>();
        while(Node != null) {
            list.add(Node.val);
            Node = Node.next;
        }
        Collections.reverse(list);
        return list;
    }
~~~





## Further

https://zihengcat.github.io/2019/05/15/java-data-structure-and-algorithm-linked-list/

[How To Reverse ArrayList In Java With Example](https://javahungry.blogspot.com/2017/09/how-to-reverse-arraylist-in-java-with-Example.html#:~:text=To reverse an ArrayList in,List type as an argument.)