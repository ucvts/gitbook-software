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
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleArrayList()`
   * `SimpleArrayList(int initialCapacity)`
   * `SimpleArrayList(Collection<String> c)`
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
   * `removeRange(int fromIndex, int toIndex)`
   * `set(int index, String s)`
   * `size()`
   * `trimToSize()`
5. Your `SimpleArrayList` class should behave exactly as the built-in `ArrayList` class does.

## Deliverables

1. Submit your repository URL.

Your implementation must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 20, 2020.

