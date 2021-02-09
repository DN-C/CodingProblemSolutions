## Description

Given an Iterator class interface with methods: `next()` and `hasNext()`, design and implement a PeekingIterator that support the `peek()` operation -- it essentially peek() at the element that will be returned by the next call to next().

**Example:**

```
Assume that the iterator is initialized to the beginning of the list: [1,2,3].

Call next() gets you 1, the first element in the list.
Now you call peek() and it returns 2, the next element. Calling next() after that still return 2. 
You call next() the final time and it returns 3, the last element. 
Calling hasNext() after that should return false.
```

**Follow up**: How would you extend your design to be generic and work with all types, not just integer?

## Thinking

Basically comes from Google's guava library source code.

## Solutions

~~~java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html

class PeekingIterator implements Iterator<Integer> {
    Iterator<Integer> iter;
    Integer next;
    boolean hasPeeked = false;
    
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
        iter = iterator;
	}
	
    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
        if(!hasPeeked) {
            next = iter.next();
            hasPeeked = true;
        }
        return next;
	}
	
	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if(!hasPeeked) {
            return iter.next();
        }
        Integer result = next;
        hasPeeked = false;
        next = null;
        return result;
	}
	
	@Override
	public boolean hasNext() {
	    return hasPeeked || iter.hasNext();
	}
}
~~~



## Further

https://github.com/google/guava/blob/703ef758b8621cfbab16814f01ddcc5324bdea33/guava-gwt/src-super/com/google/common/collect/super/com/google/common/collect/Iterators.java#L1125

https://leetcode.com/problems/peeking-iterator/discuss/72558/Concise-Java-Solution