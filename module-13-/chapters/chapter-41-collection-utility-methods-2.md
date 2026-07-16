# Chapter 41 — Collection Utility Methods (Part 2)

In the previous chapter, we studied:

* `Collections.reverse()`
* `Collections.shuffle()`

Now we will complete the main utility methods from the `Collections` class:

* `max()`
* `min()`
* `frequency()`
* `unmodifiableList()`

These methods are very common when working with collections.

---

# Part 1 — Collections.max()

Purpose:

> Find the largest element in a collection.

---

Example with numbers:

```java id="j7m3x9"
List<Integer> numbers =
        new ArrayList<>();

numbers.add(10);
numbers.add(50);
numbers.add(20);
```

---

Find maximum:

```java id="q5m8x2"
Integer max =
        Collections.max(numbers);
```

---

Result:

```text id="x8m3q6"
50
```

---

# How Does max() Know The Order?

Important question.

How does Java know:

```text id="v4m9q1"
50 > 20
```

?

The elements must have a natural ordering.

Meaning:

They implement:

```java id="m6q2x8"
Comparable
```

---

Examples:

## Integer

Already implements:

```java id="n8m3p5"
Comparable<Integer>
```

---

## String

Already implements:

```java id="r5x9m2"
Comparable<String>
```

---

Example:

```java id="z7m3q8"
List<String> names =
        List.of(
            "Carlos",
            "Ana",
            "Maria"
        );


String max =
        Collections.max(names);
```

---

Result:

```text id="p4m8x1"
Maria
```

Because alphabetical comparison:

```text id="k8m2q5"
M > C > A
```

---

# Custom Objects

Example:

```java id="w5q9m3"
List<Product> products;
```

Can only use:

```java id="x3m8q2"
Collections.max(products)
```

if:

```java id="m7q4x9"
Product implements Comparable<Product>
```

---

Example:

Product natural order:

```text id="n5m8q3"
name
```

Then:

```java id="v8q2m5"
Collections.max(products)
```

returns:

```text id="r6m3x9"
product with highest name
```

---

# Complexity

Finding maximum requires checking every element.

Therefore:

```text id="q7m2x8"
O(n)
```

---

# Part 2 — Collections.min()

Purpose:

> Find the smallest element.

---

Example:

```java id="h5m9x2"
Integer min =
        Collections.min(numbers);
```

---

List:

```text id="p8m3q6"
10
50
20
```

Result:

```text id="z4m8x1"
10
```

---

Same requirements:

Elements need:

```java id="x6m2q9"
Comparable
```

---

Complexity:

```text id="w7m3q5"
O(n)
```

---

# max() and min() With Comparator

Sometimes natural order is not enough.

Example:

Products.

Natural:

```text id="m8q3x5"
Name
```

But we want:

```text id="v5m9q2"
Highest price
```

---

Use:

```java id="c7m2x8"
Collections.max(
    products,
    comparator
);
```

---

Example:

```java id="r4m8x1"
ProductPriceComparator comparator =
        new ProductPriceComparator();


Product expensive =
        Collections.max(
            products,
            comparator
        );
```

---

Now Java compares:

```text id="k9m3q5"
price
```

instead of:

```text id="x8m2q4"
name
```

---

# Part 3 — Collections.frequency()

Purpose:

> Count how many times an element appears.

---

Example:

```java id="m5q8x3"
List<String> words =
        new ArrayList<>();

words.add("java");
words.add("python");
words.add("java");
words.add("java");
```

---

Count:

```java id="p7m3x9"
int quantity =
        Collections.frequency(
            words,
            "java"
        );
```

---

Result:

```text id="z6m2q8"
3
```

---

# How It Works

Internally:

Conceptually:

```text id="v4q9m1"
for each element

compare with target

increase counter
```

---

Complexity:

```text id="n8m3x5"
O(n)
```

---

# Real Examples

## Word Counter

Count:

```text id="x5q8m2"
java
```

appears:

```text id="m7q3x9"
25 times
```

---

## Inventory

Count:

```text id="r8m2q5"
products with same category
```

---

# Part 4 — Collections.unmodifiableList()

Now we will discuss an important concept:

> Protecting collections from modification.

---

Problem:

Imagine:

```java id="q6m3x8"
List<String> users =
        new ArrayList<>();
```

Any code can do:

```java id="w5m8x2"
users.clear();
```

or:

```java id="p3x9m4"
users.add("Admin");
```

Sometimes we need:

> A read-only view.

---

# Creating Unmodifiable List

Example:

```java id="z8m3q5"
List<String> names =
        new ArrayList<>();


names.add("John");
names.add("Maria");


List<String> readOnly =
        Collections.unmodifiableList(
            names
        );
```

---

Now:

Allowed:

```java id="x7m2q9"
readOnly.get(0);
```

---

Not allowed:

```java id="h4m8x3"
readOnly.add("Carlos");
```

---

Result:

```text id="m9q2x5"
UnsupportedOperationException
```

---

# Important Detail

unmodifiableList() does NOT create a copy.

It creates:

```text id="v5m8q1"
protected view
```

---

Example:

Original:

```java id="c8m3x9"
names
```

Read-only:

```java id="q4m7x2"
readOnly
```

Both point to the same data.

---

If original changes:

```java id="w8m2q5"
names.add("Carlos");
```

The read-only view sees:

```text id="r6m3x9"
John
Maria
Carlos
```

---

# Immutable vs Unmodifiable

Important distinction.

---

## Unmodifiable

Means:

```text id="z7m3x8"
You cannot modify through this reference.
```

But another reference may change it.

---

## Immutable

Means:

```text id="p5m8q2"
The object can never change.
```

---

Example:

```java id="x3m9q6"
List.of()
```

creates immutable lists.

---

# Common Mistakes

---

## Mistake 1 — Using max() without Comparable

Wrong:

```java id="m8q3x5"
Collections.max(products);
```

when Product has no:

```java id="v4m9x2"
Comparable
```

---

## Mistake 2 — Expecting frequency() to modify

Wrong idea:

```text id="q7m3x9"
frequency removes duplicates
```

No.

It only counts.

---

## Mistake 3 — Thinking unmodifiableList copies data

It does not.

---

# Collections Utility Summary

| Method             | Purpose           | Complexity |
| ------------------ | ----------------- | ---------- |
| reverse()          | Reverse order     | O(n)       |
| shuffle()          | Random order      | O(n)       |
| max()              | Find greatest     | O(n)       |
| min()              | Find smallest     | O(n)       |
| frequency()        | Count occurrences | O(n)       |
| unmodifiableList() | Protect list      | O(1)       |

---

# Applying To Final Project

Library Management System examples:

---

Find most borrowed book:

```text id="m5x8q3"
Collections.max()
```

---

Random book recommendation:

```text id="k7m3q9"
Collections.shuffle()
```

---

Count category occurrences:

```text id="p4m8x2"
Collections.frequency()
```

---

Protect configuration data:

```text id="z8m3q5"
Collections.unmodifiableList()
```

---

# Exercise Task

Create:

```java id="x5m9q2"
List<Integer> ratings
```

Add:

```text id="n8m3q7"
5
8
10
6
10
```

Implement:

1. Find maximum rating.
2. Find minimum rating.
3. Count how many times `10` appears.
4. Create an unmodifiable version and try adding a value.

---

# ✔️ Next Step

In **Chapter 42 — Iterator and ListIterator (Part 1)** we will learn:

* Why normal loops can fail when removing elements.
* The `Iterator` interface.
* Safe removal during iteration.
* How collections are traversed internally.
