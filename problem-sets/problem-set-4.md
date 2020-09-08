# Problem Set 4

## **Summary**

Implement a simplified, but working version of the `HashMap` class without using built-in Java library classes.

## Requirements

1. Create a new repository called `pset-4`.
2. Implement a simplified, but working version of the `HashMap` class.
3. Add, commit, and push your code to the `pset-4` repository.

## Specifications

Your code must adhere to the following specifications.

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

Your implementations must behave identically to the built-in Java library class on which it is based.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, September 27, 2020.

