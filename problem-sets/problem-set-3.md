# Problem Set 3

## **Summary**

Implement a simplified, but working version of the `Stack` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-3`.
2. Implement a simplified, but working version of the `Stack` class.
3. Add, commit, and push your code to the `pset-3` repository.

## Specifications

Your code must adhere to the following specifications.

### Stack

1. Implement a simplified, but working version of the `Stack` class called `SimpleStack` capable only of storing `String` objects.
2. You are prohibited from using any Java library classes other than `String` and `Exception` classes.
3. You must implement the following constructors, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `SimpleStack()`
4. You must implement the following methods, some of which have been modified to adhere to the simplification of only storing `String` objects.
   * `empty()`
   * `peek()`
   * `pop()`
   * `push(String item)`
   * `search(String s)`
   * `toString()`
5. Your `SimpleStack` class should behave exactly as the built-in `Stack` class does.

## Testing

Your code should behave exactly as a `Stack` would. You can use the tester class in [the solution repository](https://github.com/ucvts/pset-3-solution-5106) to put your `SimpleStack` class through the paces.

If your code works, the tester class should print the following output.

```text
PASSED: testConstructors.
PASSED: testEmpty.
PASSED: testPeek.
PASSED: testPop.
PASSED: testPush.
PASSED: testSearch.
```

If it prints any failures, you'll need to investigate these and fix them.

## Deliverables

1. Submit your repository URL.

Your implementation must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, October 4, 2020.

