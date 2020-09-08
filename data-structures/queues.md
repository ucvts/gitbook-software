# Queues

{% hint style="info" %}
* _Core Java: Volume I—Fundamentals_
  * 9.2.5 and 9.2.6
{% endhint %}

## Overview

Queues are nothing more than a line you might wait in at the store. You enter the line at the back, and you exit the line when you reach the front. Remember stacks? They operated one a LIFO \(last-in-first-out\) system. Well, queues work the other way around. It's a first-in-first-out \(FIFO\) system.

## Implementations

There are few different types of queues, namely an `AbstractQueue` and a `PriorityQueue`. An `AbstractQueue` behaves exactly as you might expect, and that's what we'll focus on.

![](../.gitbook/assets/queue.png)

### AbstractQueue

An `AbstractQueue` is pretty simple. It functions just like a line. You can add elements to the back of the queue, and remove elements from the front of it. That's about it!

And the operations it provides are equally simply. Let's take a look.

#### Constructors

There's just one way to create and `AbstractQueue`.

* `AbstractQueue()`

As you might've guessed, this creates an empty queue. You can read more about it in [the documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/AbstractQueue.html).

#### Methods

There aren't many operations to cover. The functionality isn't all that complex.

* `add(E e)`
* `clear()`
* `element()`
* `remove()`

See? Simple. Most of these are pretty self-explanation, and are [well-documented](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/AbstractQueue.html).

{% page-ref page="../problem-sets/problem-set-3.md" %}

