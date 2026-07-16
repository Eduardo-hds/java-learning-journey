# Chapter 22 — Sorting Collections: Comparator

In the previous chapter, we learned about `Comparable`.

`Comparable` answers:

> "What is the default order of this object?"

But real applications usually need multiple ways to sort the same data.

Example: A product can be sorted by:

* Name.
* Price.
* Quantity.
* Rating.
* Creation date.

We cannot put all these rules inside:

```java
compareTo()
```

For this situation, Java provides:

```java id="v0k8sa"
Comparator
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What Comparator is.
* Why Comparator exists.
* Difference between Comparable and Comparator.
* How to create custom sorting rules.
* Lambda-based comparators.
* Sorting by multiple fields.
* When to use Comparator.

---

# What is Comparator?

`Comparator` is an object that defines a custom comparison rule.

Unlike `Comparable`:

```text id="1xk4f8"
Comparable
    |
    v
Inside the class
```

Comparator:

```text id="v2p7m4"
Comparator
    |
    v
Outside the class
```

---

# Why Does Comparator Exist?

Imagine a class:

```java id="2u8m8d"
Product
```

with:

```text id="z4d0l6"
name
price
quantity
```

Possible sorting:

---

By name:

```text id="4m8g0n"
Keyboard
Monitor
Mouse
```

---

By price:

```text id="b1t6x9"
50
100
200
```

---

By quantity:

```text id="m6c9v7"
5
10
20
```

Which one is the natural order?

There is no obvious answer.

Comparator solves this.

---

# Comparator Interface

Package:

```java id="g3g8j2"
java.util.Comparator
```

Main method:

```java id="5wx7r4"
int compare(T o1, T o2);
```

---

Return rules:

| Result   | Meaning            |
| -------- | ------------------ |
| Negative | o1 comes before o2 |
| Zero     | Same order         |
| Positive | o1 comes after o2  |

---

# Example Class

We will use:

```java id="3g9j5c"
public class Product {

    private String name;
    private double price;
    private int quantity;

}
```

---

# Sorting by Name

Create a Comparator:

```java id="qf0r8c"
Comparator<Product> nameComparator =
    new Comparator<Product>() {

        @Override
        public int compare(
                Product p1,
                Product p2){

            return p1.getName()
                     .compareTo(
                         p2.getName()
                     );
        }
};
```

---

Use:

```java id="4v5p9k"
Collections.sort(
    products,
    nameComparator
);
```

Result:

```text id="5m9t2a"
Keyboard
Monitor
Mouse
```

---

# Lambda Syntax

Modern Java simplifies this.

Instead of:

```java id="9d8q0m"
new Comparator<Product>(){

}
```

Use:

```java id="u0q7v2"
Comparator<Product> nameComparator =
    (p1,p2) ->
        p1.getName()
          .compareTo(
              p2.getName()
          );
```

---

# Sorting by Price

Example:

```java id="q2x8k6"
Comparator<Product> priceComparator =
    (p1,p2) ->
        Double.compare(
            p1.getPrice(),
            p2.getPrice()
        );
```

---

Before:

```text id="0b4m4h"
Mouse     50
Monitor   200
Keyboard  100
```

After:

```text id="4m2l8x"
Mouse     50
Keyboard  100
Monitor   200
```

---

# Sorting Descending

Use reversed comparison.

Example:

```java id="n9d3k0"
Comparator<Product> priceDescending =
    (p1,p2) ->
        Double.compare(
            p2.getPrice(),
            p1.getPrice()
        );
```

Result:

```text id="5p1n6q"
Monitor
Keyboard
Mouse
```

---

# Comparator.comparing()

Java provides helper methods.

Instead of:

```java id="m5z8c7"
(p1,p2) ->
    p1.getName()
      .compareTo(p2.getName())
```

Use:

```java id="t1y7pc"
Comparator.comparing(
    Product::getName
);
```

---

Example:

```java id="f4q8y2"
products.sort(
    Comparator.comparing(
        Product::getName
    )
);
```

---

# Multiple Sorting Rules

Real systems often need:

Example:

Sort employees by:

1. Department.
2. Then salary.

Comparator supports chaining.

---

Example:

```java id="s3c9v1"
Comparator<Employee> comparator =
    Comparator
        .comparing(Employee::getDepartment)
        .thenComparing(Employee::getSalary);
```

---

Result:

```text id="t6m2h7"
IT
  Alice 3000
  Bob   5000

HR
  Maria 4000
```

---

# Reversing Order

Any Comparator can be reversed:

```java id="p8x5v0"
comparator.reversed();
```

Example:

```java id="a6m4q3"
products.sort(
    Comparator
        .comparing(Product::getPrice)
        .reversed()
);
```

---

# Comparator With List.sort()

Modern Java:

```java id="3x5z7v"
products.sort(
    priceComparator
);
```

Equivalent to:

```java id="0f3x9k"
Collections.sort(
    products,
    priceComparator
);
```

---

# Comparable vs Comparator

This comparison is fundamental.

| Feature         | Comparable   | Comparator    |
| --------------- | ------------ | ------------- |
| Location        | Inside class | Outside class |
| Method          | compareTo()  | compare()     |
| Number of rules | One          | Many          |
| Changes class   | Yes          | No            |
| Flexibility     | Lower        | Higher        |

---

# Example Design Decision

Class:

```java id="5i3n9p"
Student
```

Possible ordering:

* ID.
* Name.
* Grade.

---

## Comparable

Choose:

```text id="o4u6y8"
Student ID
```

because every system agrees:

"Students are identified by ID."

---

## Comparator

Create:

```text id="5v7k8n"
NameComparator

GradeComparator
```

for different reports.

---

# Comparator and TreeSet / TreeMap

Comparator is not only for sorting Lists.

It can define ordering in:

* TreeSet.
* TreeMap.

---

Example:

```java id="m7d9p2"
Set<Product> products =
    new TreeSet<>(
        Comparator.comparing(
            Product::getPrice
        )
    );
```

Now products are organized by price.

---

# Important: Comparator and Equality

A subtle point.

Tree collections use comparison to determine duplicates.

Example:

Comparator:

```java id="4v7n0d"
compareByName
```

Products:

```text id="g2k5n8"
Mouse 100
Mouse 200
```

Comparator result:

```text id="0b5f7w"
0
```

TreeSet may consider them equal.

Even though:

```text id="8u3x2m"
prices are different
```

---

# Advantages of Comparator

## 1. Multiple Sorting Strategies

Example:

```text id="g4x8d9"
ProductByName

ProductByPrice

ProductByStock
```

---

## 2. Does Not Modify the Class

Useful for:

* External classes.
* Libraries.

---

## 3. More Flexible

Can change sorting dynamically.

---

# Disadvantages of Comparator

## 1. More Code

Many comparators can create extra classes.

---

## 2. Possible Inconsistency

Different comparators may define different equality rules.

---

# When Should You Use Comparator?

Use when:

✅ Multiple sorting options exist.

Example:

Product reports.

---

✅ You cannot modify the class.

Example:

Third-party library objects.

---

✅ Sorting depends on context.

Example:

Admin screen:

Sort by price.

Customer screen:

Sort by popularity.

---

# When Should You NOT Use Comparator?

Avoid when:

❌ There is one obvious natural order.

Example:

A `Student` always identified by ID.

Use:

```java
Comparable
```

---

# Practical Example — Product Reports

Product:

```text id="9r6m0f"
Name: Laptop
Price: 4000
Stock: 10
```

Reports:

---

## Price Report

```java id="h4k6w1"
Comparator.comparing(
    Product::getPrice
);
```

---

## Name Report

```java id="9w2n8f"
Comparator.comparing(
    Product::getName
);
```

---

## Stock Report

```java id="f7q3s9"
Comparator.comparing(
    Product::getQuantity
);
```

Same class.

Different views.

---

# Common Mistakes

## Mistake 1 — Mixing compare values

Wrong:

```java id="x3m7u2"
return 10;
```

The return value is not the difference.

It only indicates direction.

---

## Mistake 2 — Using subtraction

Avoid:

```java id="0m4x8v"
p1.getAge() - p2.getAge()
```

Better:

```java id="h6c8q1"
Integer.compare(
    p1.getAge(),
    p2.getAge()
)
```

---

## Mistake 3 — Forgetting null values

Example:

```text id="2f6x9d"
Product name = null
```

Comparison can fail.

---

# Chapter Summary

You learned:

* Comparator defines custom sorting rules.
* It exists because objects can have multiple valid orders.
* It works outside the class.
* It supports:

  * multiple comparisons,
  * chaining,
  * reversing.
* It is heavily used in professional Java applications.

The key idea:

> Comparable defines what an object naturally is. Comparator defines how we want to view it.

---

# ✔️ Next Step

In **Chapter 23 — Collections Utility Methods**, we will study the helper methods provided by the `Collections` class, including:

* `reverse()`
* `shuffle()`
* `max()`
* `min()`
* `frequency()`
* `unmodifiableList()`

These utilities allow you to manipulate collections efficiently without reinventing common operations.
