# Problem Set 1

## **Summary**

Implement simplified, but working versions of the `ArrayList`, `LinkedList`, `Stack`, `HashSet`, `AbstractQueue`, and `HashMap` classes without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-1`.
2. Implement simplified, but working versions of the `ArrayList`, `LinkedList`, `Stack`, `HashSet`, `AbstractQueue`, and `HashMap` classes
3. Each implementation should be self-contained in its own `.java` file.
4. Add, commit, and push your code to the `pset-1` repository.

## Specifications

Your code must adhere to the following specifications for each implementation.

### ArrayList

1. Implement a simplified, but working version of the `ArrayList` class called `SimpleArrayList` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `ArrayList()`
   * `ArrayList(int initialCapacity)`
   * `ArrayList(Collection<String> c)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(int index, String element)`
   * `add(String e)`
   * `clear()`
   * `contains(String o)`
   * `get(int index)`
   * `indexOf(String o)`
   * `isEmpty()`
   * `remove(int index)`
   * `remove(String o)`
   * `removeRange(int fromIndex, int toIndex)`
   * `set(int index, String element)`
   * `size()`
   * `trimToSize()`
5. Your `SimpleArrayList` class should behave exactly as the built-in `ArrayList` class does.

### LinkedList

1. Implement a simplified, but working version of the `LinkedList` class called `SimpleLinkedList` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. Your `SimpleLinkedList` class must be doubly linked.
4. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `LinkedList()`
   * `LinkedList(Collection<String> c)`
5. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(int index, String element)`
   * `addFirst(String e)`
   * `addLast(String e)`
   * `clear()`
   * `contains(String o)`
   * `get(int index)`
   * `getFirst()`
   * `getLast()`
   * `indexOf(String o)`
   * `remove(int index)`
   * `remove(String o)`
   * `removeFirst()`
   * `removeFirstOccurrence()`
   * `removeLast()`
   * `removeLastOccurrence()`
   * `set(int index, String element)`
   * `size()`

### Stack



### HashSet



### AbstractQueue



### HashMap

## Deliverables

1. Submit your repository URL.

Your program output should match mine exactly for each of the exercises above.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 20, 2020.

