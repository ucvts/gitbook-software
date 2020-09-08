# Problem Set 1

## **Summary**

Implement simplified, but working versions of the `ArrayList`, `LinkedList`, and `Stack` classes without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-1`.
2. Implement simplified, but working versions of the `ArrayList`, `LinkedList`, and `Stack` classes.
3. Each implementation should be self-contained in its own `.java` file.
4. Add, commit, and push your code to the `pset-1` repository.

## Specifications

Your code must adhere to the following specifications for each implementation.

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

### LinkedList

1. Implement a simplified, but working version of the `LinkedList` class called `SimpleLinkedList` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. Your `SimpleLinkedList` class must be doubly linked.
4. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleLinkedList()`
   * `SimpleLinkedList(Collection<String> c)`
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
   * `removeFirstOccurrence()`
   * `removeLast()`
   * `removeLastOccurrence()`
   * `set(int index, String s)`
   * `size()`
6. Your `SimpleLinkedList` class should behave exactly as the built-in `LinkedList` class does.

### Stack

1. Implement a simplified, but working version of the `Stack` class called `SimpleStack` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleStack()`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `empty()`
   * `peek()`
   * `pop()`
   * `push(String item)`
   * `search(String s)`
5. Your `SimpleStack` class should behave exactly as the built-in `Stack` class does.

## Deliverables

1. Submit your repository URL.

Your implementations must behave identically to the built-in Java library classes on which they are based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 20, 2020.

