# Problem Set 2

## **Summary**

Implement a simplified, but working version of the `LinkedList` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-2`.
2. Implement a simplified, but working version of the `LinkedList` class.
3. Add, commit, and push your code to the `pset-2` repository.

## Specifications

Your code must adhere to the following specifications.

### LinkedList

1. Implement a simplified, but working version of the `LinkedList` class called `SimpleLinkedList` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String` and `List` \(and `List` can only be used in the second constructor\).
3. Your `SimpleLinkedList` class must be doubly linked.
4. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleLinkedList()`
   * `SimpleLinkedList(List<String> list)`
5. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(int index, String s)`
   * `addFirst(String s)`
   * `addLast(String s)`
   * `clear()`
   * `contains(String s)`
   * `get(int index)`
   * `getFirst()`
   * `getLast()`
   * `indexOf(String s)`
   * `remove(int index)`
   * `remove(String s)`
   * `removeFirst()`
   * `removeLast()`
   * `set(int index, String s)`
   * `size()`
   * `toString()`
6. Your `SimpleLinkedList` class should behave exactly as the built-in `LinkedList` class does.

## Testing

Your code should behave exactly as a `LinkedList` would. You can use the tester class in [the solution repository](https://github.com/ucvts/pset-2-solution-5106) to put your `SimpleLinkedList` class through the paces.

If your code works, the tester class should print the following output.

```text
PASSED: testConstructors.
PASSED: testAdd.
PASSED: testSizeAndClear.
PASSED: testContainsAndIndexOf.
PASSED: testGet.
PASSED: testRemove.
PASSED: testSet.
```

If it prints any failures, you'll need to investigate these and fix them.

## Deliverables

1. Submit your repository URL.

Your implementation must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 20, 2020.

