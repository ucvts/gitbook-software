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

### HashSet

1. Implement a simplified, but working version of the `HashSet` class called `SimpleHashSet` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleHashSet()`
   * `SimpleHashSet(int initialCapacity)`
   * `SimpleHashSet(Collection<String> c)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(String s)`
   * `clear()`
   * `contains(String s)`
   * `isEmpty()`
   * `remove(String s)`
   * `size()`
5. Your `SimpleHashSet` class should behave exactly as the built-in `HashSet` class does.

### AbstractQueue

1. Implement a simplified, but working version of the `AbstractQueue` class called `SimpleAbstractQueue` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleAbstractQueue()`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(String s)`
   * `clear()`
   * `element()`
   * `remove()`
5. Your `SimpleAbstractQueue` class should behave exactly as the built-in `AbstractQueue` class does.

### HashMap

1. Implement a simplified, but working version of the `HashMap` class called `SimpleHashMap` capable only of using `String` objects as the keys and values.
2. You are prohibited from using any Java library classes other than `String`.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only using `String` objects as the keys and values.
   * `SimpleHashMap()`
   * `SimpleHashMap(int initialCapacity)`
   * `SimpleHashMap(Map<String, String> m)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only using `String` objects as the keys and values.
   * `clear()`
   * `containsKey(String key)`
   * `containsValue(String value)`
   * `get(String key)`
   * `isEmpty()`
   * `keySet()`
   * `put(String key, String value)`
   * `remove(String key)`
   * `size()`
   * `values()`
5. Your `SimpleHashMap` class should behave exactly as the built-in `HashMap` class does.

## Deliverables

1. Submit your repository URL.

Your implementations must behave identically to the built-in Java library classes on which they are based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 27, 2020.

