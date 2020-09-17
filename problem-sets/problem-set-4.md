# Problem Set 4

## **Summary**

Implement a simplified, but working version of the `ArrayBlockingQueue` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-4`.
2. Implement a simplified, but working version of the `ArrayBlockingQueue` class.
3. Add, commit, and push your code to the `pset-4` repository.

## Specifications

Your code must adhere to the following specifications.

### ArrayBlockingQueue

1. Implement a simplified, but working version of the `ArrayBlockingQueue` class called `SimpleQueue` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String` and `Exception` classes.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleQueue(int initialCapacity)`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `add(String s)`
   * `clear()`
   * `contains(String s)`
   * `element()`
   * `offer(String s)`
   * `peek()`
   * `poll()`
   * `remainingCapacity()`
   * `remove()`
   * `remove(String s)`
   * `size()`
   * `toString()`
5. Your `SimpleQueue` class should behave exactly as the built-in `ArrayBlockingQueue` class does.

## Testing

Your code should behave exactly as an `ArrayBlockingQueue` would. You can use [the tester class in the solution repository](https://github.com/ucvts/pset-4-solution-5106) to put your `SimpleQueue` class through the paces.

If your code works, the tester class should print the following output.

```text
PASSED: testConstructors.
PASSED: testAddAndOffer.
PASSED: testClear.
PASSED: testContains.
PASSED: testElementAndPeek.
PASSED: testPollAndRemove.
```

If it prints any failures, you'll need to investigate these and fix them.

## Deliverables

1. Submit your repository URL.

Your implementation must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, October 11, 2020.

