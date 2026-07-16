# Chapter 02 — The `List` Interface

Now that you understand the architecture of the Java Collections Framework, it's time to study the first—and arguably most commonly used—collection type: the **`List`**.

If you've ever worked with:

* a shopping cart,
* a list of students,
* messages in a chat,
* products in an inventory,
* books in a library,

then you've already encountered problems that are naturally modeled as a **List**.

---

# Learning Objectives

By the end of this chapter, you should be able to:

* Explain what the `List` interface is.
* Understand why it exists.
* Describe its characteristics.
* Perform common `List` operations.
* Understand how indexing works.
* Compare `List` with arrays and `Set`.
* Know when a `List` is the appropriate choice.

---

# What is a List?

A **List** is an **ordered collection** of elements.

It preserves the position of every element.

Example:

```text
Index

0 → Alice
1 → Bob
2 → Charlie
3 → David
```

Unlike a `Set`, the position of each element matters.

---

# Why Does List Exist?

Arrays already allow indexed access.

So why create another structure?

Because arrays are **fixed in size**.

A `List` provides:

* dynamic resizing,
* automatic insertion,
* automatic removal,
* rich manipulation methods.

Instead of writing:

```java
Student[] students = new Student[100];
```

you can simply write:

```java
List<Student> students = new ArrayList<>();
```

Now Java manages the storage for you.

---

# The List Contract

`List` is an **interface**.

It defines behaviors that every implementation must provide.

Some of the most important methods are:

```java
add(E element)
```

```java
remove(int index)
```

```java
remove(Object element)
```

```java
get(int index)
```

```java
set(int index, E element)
```

```java
contains(Object o)
```

```java
size()
```

```java
isEmpty()
```

```java
clear()
```

Notice that the interface specifies **what** can be done—not **how** it is implemented.

---

# Characteristics of a List

Every `List` has several important properties.

## 1. Ordered

Elements remain in insertion order unless you explicitly change it.

Example:

```java
List<String> names = new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Result:

```text
0 Alice
1 Bob
2 Charlie
```

The order is preserved.

---

## 2. Indexed

Every element has an index.

```java
System.out.println(names.get(1));
```

Output:

```text
Bob
```

Just like arrays.

---

## 3. Allows Duplicates

Unlike `Set`, a `List` accepts repeated elements.

Example:

```java
names.add("Alice");
```

Result:

```text
Alice
Bob
Charlie
Alice
```

Both `"Alice"` entries are stored.

This is perfectly valid.

---

## 4. Dynamic Size

Lists grow automatically.

```java
List<Integer> numbers = new ArrayList<>();

numbers.add(10);
numbers.add(20);
numbers.add(30);
numbers.add(40);
numbers.add(50);
```

No need to define a maximum size in advance.

---

# Internal Implementation

The `List` interface itself has **no internal implementation**.

Instead, classes such as:

* `ArrayList`
* `LinkedList`

provide different implementations of the same contract.

Think of it like this:

```text
           List
            ▲
      ┌─────┴─────┐
      │           │
 ArrayList   LinkedList
```

Both are Lists.

They simply organize data differently.

We'll study each implementation separately.

---

# Creating a List

The recommended approach is:

```java
List<String> names = new ArrayList<>();
```

Notice that the variable type is the interface (`List`).

This gives flexibility.

Later, if necessary, changing the implementation is easy:

```java
List<String> names = new LinkedList<>();
```

The rest of your code usually remains unchanged.

---

# Basic Operations

## Adding Elements

```java
List<String> names = new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Result:

```text
[Alice, Bob, Charlie]
```

---

## Accessing Elements

```java
System.out.println(names.get(0));
```

Output:

```text
Alice
```

---

## Updating Elements

```java
names.set(1, "Brian");
```

Result:

```text
[Alice, Brian, Charlie]
```

---

## Removing by Index

```java
names.remove(0);
```

Result:

```text
[Brian, Charlie]
```

---

## Removing by Value

```java
names.remove("Charlie");
```

Result:

```text
[Brian]
```

---

## Searching

```java
System.out.println(names.contains("Brian"));
```

Output:

```text
true
```

---

## Number of Elements

```java
System.out.println(names.size());
```

Output:

```text
1
```

Notice that `size()` returns the number of stored elements, not the internal capacity.

---

## Clearing the List

```java
names.clear();
```

Result:

```text
[]
```

---

# Iterating Through a List

The most common approach is the enhanced `for` loop.

```java
for (String name : names) {
    System.out.println(name);
}
```

Output:

```text
Alice
Bob
Charlie
```

You can also use a traditional `for` loop when you need the index.

```java
for (int i = 0; i < names.size(); i++) {
    System.out.println(i + " -> " + names.get(i));
}
```

Output:

```text
0 -> Alice
1 -> Bob
2 -> Charlie
```

We'll later explore `Iterator` and `ListIterator`, which are safer when modifying a collection during iteration.

---

# Time Complexity (Conceptual)

Because `List` is only an interface, it doesn't define performance.

Different implementations have different costs.

Conceptually:

| Operation       | Depends on Implementation |
| --------------- | ------------------------- |
| Add             | Yes                       |
| Remove          | Yes                       |
| Search          | Yes                       |
| Access by Index | Yes                       |

We'll analyze the exact complexities for `ArrayList` and `LinkedList` in the next chapters.

---

# Memory Considerations

The `List` interface itself doesn't consume memory.

Memory usage depends entirely on the chosen implementation.

For example:

* `ArrayList` stores elements in a dynamic array.
* `LinkedList` stores elements in linked nodes.

These internal differences affect performance and memory consumption.

---

# Advantages

* Preserves insertion order.
* Supports indexed access.
* Allows duplicate elements.
* Automatically grows.
* Rich API.
* Easy to use.
* Suitable for most business applications.

---

# Disadvantages

* Duplicate elements may be undesirable in some scenarios.
* Searching is not always efficient.
* Some implementations consume more memory.
* Choosing the wrong implementation can impact performance.

---

# When Should You Use a List?

A `List` is the right choice when:

* Order matters.
* Duplicate elements are allowed.
* You need indexed access.
* Elements may be added or removed over time.

Examples:

* Student lists
* Shopping carts
* Product catalogs
* Chat messages
* Music playlists
* To-do lists
* Search history

---

# When Should You NOT Use a List?

Avoid a `List` when:

* Elements must be unique → use a `Set`.
* You need fast lookup by key → use a `Map`.
* Processing follows FIFO order → use a `Queue`.
* Data is fixed in size and performance is critical → use an array.

Choosing the correct collection makes your code more expressive and often more efficient.

---

# Common Mistakes

### Mistake 1

Using the implementation as the variable type.

Instead of:

```java
ArrayList<String> names = new ArrayList<>();
```

Prefer:

```java
List<String> names = new ArrayList<>();
```

This follows the "program to interfaces" principle.

---

### Mistake 2

Accessing an invalid index.

```java
names.get(5);
```

If the list has fewer elements, Java throws an `IndexOutOfBoundsException`.

Always ensure the index is valid.

---

### Mistake 3

Confusing `size()` with an array's `length`.

Arrays:

```java
array.length
```

Lists:

```java
list.size()
```

---

### Mistake 4

Expecting duplicates to be removed automatically.

A `List` allows duplicates.

If uniqueness is required, use a `Set`.

---

# Practical Example

Imagine a classroom application.

```java
List<String> students = new ArrayList<>();

students.add("Alice");
students.add("Bob");
students.add("Charlie");

students.remove("Bob");

students.add("David");

for (String student : students) {
    System.out.println(student);
}
```

Output:

```text
Alice
Charlie
David
```

The code is simple, readable, and leverages the `List` interface without worrying about internal storage details.

---

# Chapter Summary

In this chapter, you learned that:

* `List` is an interface representing an ordered collection.
* Lists preserve insertion order and support indexed access.
* Duplicates are allowed.
* Lists grow dynamically.
* The interface defines a contract that multiple classes implement.
* `ArrayList` and `LinkedList` are the two primary implementations.
* Choosing `List` is appropriate when order and indexing matter.

This chapter provides the conceptual foundation needed before exploring the internal mechanics and performance characteristics of the two most important `List` implementations.

---

# ✔️ Next Step

In **Chapter 03 — `ArrayList`**, we'll dive into the most widely used collection in Java. You'll learn how it works internally, how it manages dynamic resizing, why it offers fast indexed access, its time complexity for common operations, and when it should—or should not—be your default choice.
