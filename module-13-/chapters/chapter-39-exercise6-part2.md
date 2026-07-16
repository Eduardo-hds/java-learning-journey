# Chapter 39 — Exercise 6: Sorting Practice (Part 2)

In the previous chapter, we learned:

* Natural ordering.
* `Comparable`.
* `compareTo()`.
* `Collections.sort()`.

We created one default ordering for `Product`:

```text id="m8x2q7"
Product → sorted by name
```

But real applications rarely need only one sorting rule.

A product can be sorted by:

* Name.
* Price.
* Quantity.
* ID.

We cannot create multiple `compareTo()` methods.

For this problem, Java provides:

```java id="q5m8x3"
Comparator
```

---

# Comparable vs Comparator

This distinction is extremely important.

---

# Comparable

The object defines its own natural order.

Example:

```java id="z8m3q1"
Product

natural order:
name
```

The class says:

> "This is how products should normally be compared."

---

Implementation:

```java
class Product
        implements Comparable<Product>
```

Inside:

```java
compareTo()
```

---

# Comparator

A separate object defines a sorting rule.

Meaning:

> "Sort this collection using this specific strategy."

---

Example:

```text id="w7m2x9"
Sort products by:

Price
Quantity
Name
```

Without modifying Product.

---

# Real World Example

Imagine an online store.

The same products can be displayed as:

### Default

```text id="v5q8m2"
A-Z
```

---

### Cheapest first

```text id="n4m9x3"
$10
$20
$50
```

---

### Best stock availability

```text id="k8m3q5"
100 units
50 units
10 units
```

---

One class.

Multiple sorting strategies.

That is Comparator.

---

# Comparator Interface

Java provides:

```java id="m7x3q9"
Comparator<T>
```

---

Main method:

```java id="p5m8x2"
compare()
```

---

Structure:

```java id="c8q3m5"
public int compare(
        Product p1,
        Product p2
)
```

---

Same return rules:

Negative:

```text id="x4m9q2"
p1 before p2
```

Zero:

```text id="j7m3x8"
same order
```

Positive:

```text id="r5q8m1"
p1 after p2
```

---

# Sorting Products By Price

Create:

```text id="w8m2q6"
util/
 └── ProductPriceComparator.java
```

---

Class:

```java id="t3m9x5"
public class ProductPriceComparator
        implements Comparator<Product>
```

---

Implement:

```java id="q8m4x2"
@Override
public int compare(
        Product p1,
        Product p2){

    return Double.compare(
            p1.getPrice(),
            p2.getPrice()
    );

}
```

---

# Why Double.compare()?

Avoid:

```java id="f7m3x9"
p1.getPrice() - p2.getPrice()
```

because:

* Floating point precision problems.
* Incorrect conversions.

---

# Using Comparator

Example:

```java id="m2x8q5"
Collections.sort(
    products,
    new ProductPriceComparator()
);
```

---

Before:

```text id="v4q9m1"
Keyboard 150
Mouse 50
Monitor 300
```

---

After:

```text id="z6m3x8"
Mouse 50
Keyboard 150
Monitor 300
```

---

# Lambda Introduction

Later modules will cover lambdas deeply.

For now, understand this shorter syntax:

```java id="q5m8x2"
products.sort(
    (p1,p2) ->
        Double.compare(
            p1.getPrice(),
            p2.getPrice()
        )
);
```

---

Same logic.

Less code.

---

# List.sort()

Java also provides:

```java id="h8m3q5"
list.sort(comparator);
```

Example:

```java id="x7m2q9"
products.sort(
    new ProductPriceComparator()
);
```

---

Comparison:

## Collections.sort()

```java id="p3m8x1"
Collections.sort(
    list,
    comparator
);
```

---

## List.sort()

```java id="w5q9m2"
list.sort(
    comparator
);
```

---

Modern Java often prefers:

```java id="n4m7x3"
List.sort()
```

because sorting belongs naturally to the List.

---

# Creating More Comparators

---

# Sort By Name

```java id="g8m3q5"
public class ProductNameComparator
        implements Comparator<Product>{

    @Override
    public int compare(
            Product p1,
            Product p2){

        return p1.getName()
                .compareTo(
                    p2.getName()
                );

    }

}
```

---

Result:

```text id="r6m2x8"
Keyboard
Monitor
Mouse
```

---

# Sort By Quantity

```java id="m9x3q7"
public class ProductQuantityComparator
        implements Comparator<Product>{

    @Override
    public int compare(
            Product p1,
            Product p2){

        return Integer.compare(
                p1.getQuantity(),
                p2.getQuantity()
        );

    }

}
```

---

Result:

```text id="k5m8q2"
Mouse 5
Keyboard 10
Monitor 20
```

---

# Project Structure Update

Now:

```text id="v3m8q5"
src/
│
├── model/
│   └── Product.java
│
├── service/
│
└── util/
    ├── ProductPriceComparator.java
    ├── ProductNameComparator.java
    └── ProductQuantityComparator.java
```

---

# Why Put Comparators In util?

Because they are:

* Reusable.
* Independent rules.
* Not business entities.

---

# Comparing Approaches

## Comparable

Product:

```java id="x8m3q2"
implements Comparable<Product>
```

Order:

```text id="q7m9x4"
Only one default
```

---

## Comparator

Separate classes:

```text id="p5m8x3"
Many strategies
```

---

# When To Use Comparable

Use when:

The order is obvious.

Examples:

Student:

```text id="r3m7q9"
ID
```

Employee:

```text id="z6m2x8"
Name
```

---

# When To Use Comparator

Use when:

Multiple orders exist.

Examples:

Product:

```text id="m8q3x5"
Price
Name
Quantity
```

Employee:

```text id="v4m9x1"
Salary
Department
Age
```

---

# Common Mistakes

---

## Mistake 1 — Creating many Comparable rules

Wrong idea:

```text id="x3m8q5"
compareTo by name

then

compareTo by price
```

Impossible.

A class can only have one natural order.

---

## Mistake 2 — Sorting without defining comparison

Java cannot know:

```text id="k7m2x9"
Which product comes first?
```

---

## Mistake 3 — Comparator modifying objects

Comparator only decides order.

It should not change:

```java id="p8m3x5"
product.price
```

---

# Exercise Task

Create:

```text id="w6m2q8"
ProductNameComparator
ProductPriceComparator
ProductQuantityComparator
```

Test:

Products:

```text id="c9m4x7"
Mouse     50    20
Keyboard  150   10
Monitor   300   5
```

Sort by:

1. Name.
2. Price.
3. Quantity.

---

# Concepts Completed

You learned:

✅ Comparable
✅ compareTo()
✅ Comparator
✅ compare()
✅ Collections.sort()
✅ List.sort()
✅ Multiple sorting strategies

---

# ✔️ Next Step

In **Chapter 40 — Collection Utility Methods (Part 1)** we will learn the `Collections` helper class:

* `reverse()`
* `shuffle()`
* `max()`
* `min()`
* `frequency()`

and understand why Java provides utility methods separate from collection implementations.
