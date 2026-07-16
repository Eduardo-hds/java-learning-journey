# Chapter 38 — Exercise 6: Sorting Practice (Part 1)

Until now, we learned how to store and retrieve objects using collections.

But collections often need another operation:

> Organizing elements according to some rule.

Examples:

* Products by price.
* Students by grade.
* Employees by name.
* Tasks by priority.

Java provides several ways to sort objects.

In this exercise, we will learn:

* Natural ordering.
* `Comparable`.
* `compareTo()`.
* `Collections.sort()`.

---

# Exercise Objective

Create a product sorting system.

The system should allow sorting products by their natural order.

First question:

> What should be the default order of a Product?

---

# What Is Natural Ordering?

Natural ordering means:

> The default way an object compares itself to another object.

Examples:

Numbers:

```text id="4b8g4f"
1
2
3
```

Strings:

```text id="7x3m9q"
Apple
Banana
Orange
```

---

But custom objects?

Example:

```java id="p3m8x2"
Product
```

Java does not know:

Should products be sorted by:

* name?
* price?
* quantity?
* ID?

We must define it.

---

# Comparable Interface

Java provides:

```java id="q5m8x1"
Comparable<T>
```

Meaning:

> This class knows how to compare itself.

---

Hierarchy:

```text id="r7m3x9"
Object

   ↑

Comparable
```

---

# Comparable Method

The interface requires:

```java id="m4x8q2"
compareTo()
```

---

Example:

```java id="z8m2p5"
public int compareTo(Product other)
```

---

The result:

## Negative number

Current object comes first.

Example:

```text id="n5q8m3"
A before B
```

---

## Zero

Objects are equal in ordering.

---

## Positive number

Current object comes after.

Example:

```text id="x7m3q9"
B before A
```

---

# Product Sorting Example

Current Product:

```java id="g5m8x2"
public class Product {

    private int id;
    private String name;
    private double price;
    private int quantity;

}
```

---

Question:

Natural order:

```text id="j3q9m6"
Sort products by name
```

Why?

Because names are usually the most natural representation.

Example:

```text id="w8m2x5"
Keyboard
Monitor
Mouse
```

---

# Step 1 — Implement Comparable

Modify:

```java id="u4m9x2"
public class Product
        implements Comparable<Product>
```

---

Now Java expects:

```java id="m7q3x8"
compareTo()
```

---

# Step 2 — Implement compareTo()

```java id="p8x3m5"
@Override
public int compareTo(Product other){

    return this.name.compareTo(
            other.name
    );

}
```

---

# What Happens?

Example:

```text id="z5m2q7"
Keyboard.compareTo(Mouse)
```

String comparison:

```text id="x9m3q8"
Keyboard
comes before
Mouse
```

returns:

negative number.

---

# String Comparable

Important:

`String` already implements:

```java id="v3q8m1"
Comparable<String>
```

So:

```java id="a7m4x9"
name.compareTo(other.name)
```

already works.

---

# Step 3 — Create Product List

Example:

```java id="h5q8m3"
List<Product> products =
        new ArrayList<>();
```

---

Add:

```java id="t9m2x6"
products.add(
    new Product(
        1,
        "Mouse",
        50,
        10
    )
);


products.add(
    new Product(
        2,
        "Keyboard",
        150,
        5
    )
);
```

---

Current order:

```text id="q4m8x1"
Mouse
Keyboard
```

---

# Step 4 — Collections.sort()

Java provides:

```java id="c7m3x9"
Collections.sort(list);
```

---

Example:

```java id="r5x8m2"
Collections.sort(products);
```

---

Java internally calls:

```text id="w2m9q4"
compareTo()
```

---

Result:

```text id="k8m3x5"
Keyboard
Mouse
```

---

# How Sorting Works

Simplified:

```text id="f9q2m6"
Collections.sort()

        |

        v

compare objects

        |

        v

compareTo()

        |

        v

new order
```

---

# Complexity

Modern Java sorting uses optimized algorithms.

For lists:

Approximately:

```text id="n6m3x8"
O(n log n)
```

---

Why?

Because sorting requires comparing elements repeatedly.

---

# Memory Considerations

Sorting usually:

* Rearranges the existing list.
* Does not create another collection.

Example:

Before:

```text id="p7m4x2"
products
```

After:

```text id="z8q3m5"
same products
sorted
```

---

# Common Mistakes

---

## Mistake 1 — Forgetting Comparable

Without:

```java id="m4x8q2"
implements Comparable
```

This:

```java id="h7q3m9"
Collections.sort(products);
```

fails.

---

## Mistake 2 — Returning wrong values

Wrong:

```java id="x5m9q2"
return 1;
```

Always.

This breaks sorting.

---

Correct:

```java id="d8m3x7"
return this.name.compareTo(
        other.name
);
```

---

## Mistake 3 — Confusing Comparable and Comparator

Comparable:

```text id="v2q8m5"
Object defines its own order
```

Comparator:

```text id="p6m3x9"
External sorting rule
```

We will study Comparator next.

---

# Where Comparable Fits

Good examples:

## Student

Natural order:

```text id="z3m8q5"
Student ID
```

---

## Product

Natural order:

```text id="w7x2m9"
Name
```

---

## Employee

Natural order:

```text id="r4m8x3"
Name
```

---

# Exercise Task

Modify:

```text id="m5q8x2"
Product.java
```

Implement:

* `Comparable<Product>`
* `compareTo()`

Sort:

```java id="k9m3x5"
List<Product>
```

using:

```java id="h4q8m2"
Collections.sort()
```

---

Test:

Create:

```text id="x8m2q6"
Mouse
Keyboard
Monitor
```

Before:

```text id="n7q3m9"
Mouse
Keyboard
Monitor
```

After:

```text id="p5m8x2"
Keyboard
Monitor
Mouse
```

---

# ✔️ Next Step

In **Chapter 39 — Exercise 6: Sorting Practice (Part 2)** we will learn:

* `Comparator`
* Multiple sorting strategies
* Sort products by:

  * name
  * price
  * quantity
* `List.sort()`

This is where we learn why `Comparator` is usually preferred in real applications.
