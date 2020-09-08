# Sets

{% hint style="info" %}
* _Core Java: Volume I—Fundamentals_
  * 9.2.3
{% endhint %}

## Overview

Sets are similar to lists in that they store values. There are a few notable exceptions in the way restrict data, as well as how they are typically used. Sets only allow for unique values, which means unlike lists, you cannot have duplicates. As a programmer, you'll more often find yourself testing for membership in a set, rather than retrieving specific values from it \(like you would with a list\).

## Implementations

There are a number of concrete implementations of the `Set` interface, including `HashSet`, `LinkedHashSet`, and `TreeSet`. Each implementation offers its own set of positives, as well as some drawbacks. We're going to take a look at one of the most popular.

### HashSet

A `HashSet` uses something called a hash table to store values. While it may be beyond the scope of this course, values are hashed before being stored in a `HashSet`. Hashing is a process by which values of different sizes are converted to a standard size, and this is used to index the values.

Let's take a look at creating and using a `HashSet`.

#### Constructors

There are four `HashSet` constructors, but we're going to focus on only three of them.

* `HashSet()`
* `HashSet(int initialCapacity)`
* `HashSet(Collection<? extends E> c)`

Check out [the documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashSet.html) for this, but they do more or less what we've seen other constructors do.

#### Methods

Much like the list structures we've already seen, a HashSet provides a number of ways with which we can use and interact with the data. There are a few more than listed here, but these are the highlights.

* `add(E e)`
* `clear()`
* `contains(Object o)`
* `isEmpty()`
* `remove(Object o)`
* `size()`

[The documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashSet.html) is always helpful, but by now I imagine you can figure out what these do.

