# Problem Set 1

## **Summary**

Implement a simplified, but working version of the `ArrayList` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-1`.
2. Implement a simplified, but working version of the `ArrayList` class.
3. Add, commit, and push your code to the `pset-1` repository.

## Specifications

Your code must adhere to the following specifications.

### ArrayList

1. Implement a simplified, but working version of the `ArrayList` class called `SimpleArrayList` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`, `List` \(and `List` can only be used in the third constructor\), and `Exception` classes.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleArrayList()`
   * `SimpleArrayList(int initialCapacity)`
   * `SimpleArrayList(List<String> list)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(int index, String s)`
   * `add(String s)`
   * `clear()`
   * `contains(String s)`
   * `get(int index)`
   * `indexOf(String s)`
   * `isEmpty()`
   * `remove(int index)`
   * `remove(String s)`
   * `set(int index, String s)`
   * `size()`
   * `trimToSize()`
   * `toString()`
5. Your `SimpleArrayList` class should behave exactly as the built-in `ArrayList` class does.

## Testing

Your code should behave exactly as an `ArrayList` would. You can use the tester class in the solution repository to put your `SimpleArrayList` class through the paces.

If your code works, the tester class should print the following output.

```text
PASSED: testConstructors.
PASSED: testAdd.
PASSED: testClearAndIsEmpty.
PASSED: testContains.
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

