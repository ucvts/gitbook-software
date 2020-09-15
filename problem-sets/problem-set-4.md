# Problem Set 4

## **Summary**

Implement a simplified, but working version of the `PrioritQueue` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-4`.
2. Implement a simplified, but working version of the `PriorityQueue` class.
3. Add, commit, and push your code to the `pset-4` repository.

## Specifications

Your code must adhere to the following specifications.

### AbstractQueue

1. Implement a simplified, but working version of the `PriorityQueue` class called `SimpleQueue` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String`, `List` \(and `List` can only be used in the third constructor\), and `Exception` classes.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleQueue()`
   * `SimpleQueue(int initialCapacity)`
   * `SimpleQueue(List<String> list)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(E e)`
   * `clear()`
   * `comparator()`
   * `contains(Object o)`
   * `element()`
   * `offer(E e)`
   * `peek()`
   * `poll()`
   * `remove()`
   * `remove(Object o)`
   * `toString()`
5. Your `SimpleQueue` class should behave exactly as the built-in `PriorityQueue` class does.

## Testing

Your code should behave exactly as a `PriorityQueue` would. You can use the tester class in the solution repository to put your `SimpleQueue` class through the paces.

If your code works, the tester class should print the following output.

```text

```

If it prints any failures, you'll need to investigate these and fix them.

## Deliverables

1. Submit your repository URL.

Your implementation must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, October 11, 2020.

