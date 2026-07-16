# Chapter 21 — Sorting Collections: Comparable

So far in the Collections Framework, we learned how to store and retrieve data.

Now we need to solve another common problem:

> How do we organize objects in a specific order?

Examples:

* Sort students by name.
* Sort products by price.
* Sort employees by salary.
* Sort books by title.

Java provides two main approaches:

1. `Comparable`
2. `Comparator`

In this chapter, we focus on:

```java
Comparable
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* Why sorting objects is necessary.
* What natural ordering means.
* How `Comparable` works.
* The `compareTo()` method.
* How collections use Comparable.
* Advantages and limitations of Comparable.
* When to use Comparable.

---

# Why Do We Need Sorting?

Primitive values already know how to compare.

Example:

```java
5 > 3
```

Java knows:

```text
5 is greater
```

---

But objects?

Example:

```java
Student student1;
Student student2;
```

Java asks:

> "How should I compare these two objects?"

Should it compare by:

* Name?
* Age?
* Grade?
* ID?

There is no universal answer.

---

# Natural Ordering

`Comparable` defines the:

```text
Natural Order
```

of an object.

Meaning:

> The default way this object should be sorted.

---

Examples:

## String

Natural order:

```text
Alphabetical
```

Example:

```text
Alice
Bob
Carlos
```

---

## Integer

Natural order:

```text
Numerical
```

Example:

```text
1
2
3
```

---

For custom classes, we define it.

---

# Comparable Interface

Package:

```java
java.lang
```

(No import required)

Definition:

```java
public interface Comparable<T>{

    int compareTo(T other);

}
```

---

The method:

```java
compareTo()
```

returns:

| Result   | Meaning                           |
| -------- | --------------------------------- |
| Negative | Current object comes before other |
| Zero     | Objects are equal in ordering     |
| Positive | Current object comes after other  |

---

# Example: Student Sorting

Imagine:

```java
public class Student {

    private String name;
    private int age;

}
```

Java does not know:

```text
Student A < Student B?
```

We decide:

> Students are sorted by name.

---

# Implement Comparable

```java
public class Student 
        implements Comparable<Student>{

    private String name;
    private int age;


    @Override
    public int compareTo(Student other){

        return this.name.compareTo(other.name);

    }

}
```

---

Now Student has a natural order:

```text
name alphabetically
```

---

# Using Comparable With Collections.sort()

Example:

```java
List<Student> students =
        new ArrayList<>();

students.add(
    new Student("Carlos",20)
);

students.add(
    new Student("Alice",22)
);

students.add(
    new Student("Bob",21)
);
```

Before sorting:

```text
Carlos
Alice
Bob
```

---

Sort:

```java
Collections.sort(students);
```

After:

```text
Alice
Bob
Carlos
```

---

# How Collections.sort() Works

Conceptually:

```text
Collection

     |
     v

compareTo()

     |
     v

Ordering decision
```

For each comparison:

```java
student1.compareTo(student2);
```

---

# CompareTo Examples

## Alphabetical

```java
return name.compareTo(other.name);
```

Example:

```text
Alice vs Bob
```

Result:

```text
negative
```

Because Alice comes first.

---

## Numerical

Example:

Sort by age:

```java
@Override
public int compareTo(Student other){

    return Integer.compare(
        this.age,
        other.age
    );

}
```

---

Before:

```text
25
18
30
```

After:

```text
18
25
30
```

---

# Comparable and Tree Collections

Comparable is not only for sorting lists.

It is also used by:

* TreeSet
* TreeMap

Example:

```java
Set<Student> students =
        new TreeSet<>();
```

TreeSet needs to know:

```text
Where should this object be placed?
```

It uses:

```java
compareTo()
```

---

# Comparable Example With Product

Imagine:

```java
public class Product 
implements Comparable<Product>{

    private String name;
    private double price;

}
```

Natural order:

```text
price
```

Implementation:

```java
@Override
public int compareTo(Product other){

    return Double.compare(
        this.price,
        other.price
    );

}
```

Now:

```java
Collections.sort(products);
```

Sorts by price.

---

# Advantages of Comparable

## 1. Simple

The class defines its own order.

---

## 2. Works Everywhere

Compatible with:

* Collections.sort()
* TreeSet
* TreeMap

---

## 3. Consistent

Everywhere the object appears:

```text
same ordering
```

---

# Disadvantages of Comparable

## 1. Only One Natural Order

Problem:

Product can be sorted by:

* Name.
* Price.
* Quantity.

But Comparable allows only one.

Example:

```java
compareTo()
```

cannot represent all possibilities.

---

## 2. Modifies the Class

You must change:

```java
class Product
```

to:

```java
implements Comparable
```

Sometimes you cannot.

Example:

External library class.

---

# Comparable vs Comparator Preview

| Comparable       | Comparator         |
| ---------------- | ------------------ |
| Inside the class | Outside the class  |
| Natural order    | Custom orders      |
| One sorting rule | Many sorting rules |
| compareTo()      | compare()          |

---

# Example Problem

Product:

```text
Notebook
Price: 3000
Quantity: 5
```

Possible sorting:

## Option 1

Default:

```text
Price
```

Comparable:

```java
compareTo()
```

---

## Option 2

Reports:

```text
Name
```

Comparator:

```java
Comparator<Product>
```

---

# Common Mistakes

---

## Mistake 1 — Returning wrong values

Wrong:

```java
return 1;
```

for everything.

Why?

Because Java cannot know ordering.

---

## Mistake 2 — Subtraction comparison

Common:

```java
return this.age - other.age;
```

Problem:

Large numbers can overflow.

Better:

```java
return Integer.compare(
    this.age,
    other.age
);
```

---

## Mistake 3 — Making inconsistent comparisons

Example:

```java
compareTo()
```

says:

```text
A == B
```

but:

```java
equals()
```

says:

```text
A != B
```

This can cause problems in:

* TreeSet.
* TreeMap.

---

# Comparable With TreeSet Example

```java
Set<Student> students =
        new TreeSet<>();

students.add(
    new Student("Bob")
);

students.add(
    new Student("Alice")
);
```

TreeSet automatically sorts:

```text
Alice
Bob
```

because Student defines:

```java
compareTo()
```

---

# Time Complexity of Sorting

Sorting a list:

```text
O(n log n)
```

because algorithms like TimSort are used internally.

---

# Memory Considerations

Sorting generally:

* Requires temporary memory.
* Does not duplicate objects.
* Reorders references.

Example:

Before:

```text
[Student1][Student2][Student3]
```

After:

```text
[Student2][Student1][Student3]
```

Objects remain the same.

---

# When Should You Use Comparable?

Use when:

✅ The object has an obvious natural order.

Examples:

* Student by ID.
* Product by price.
* Employee by ID.

---

# When Should You NOT Use Comparable?

Avoid when:

❌ The object has multiple valid sorting rules.

Example:

Product:

* Price.
* Name.
* Quantity.

Use:

```java
Comparator
```

instead.

---

# Chapter Summary

You learned:

* Objects need rules to be sorted.
* Comparable defines natural ordering.
* `compareTo()` controls comparisons.
* Collections.sort() uses Comparable.
* TreeSet and TreeMap depend on comparison.
* Comparable provides one default ordering.

The key idea:

> Comparable answers: "What is the natural order of this object?"

---

# ✔️ Next Step

In **Chapter 22 — Sorting Collections: Comparator**, we will learn how to create multiple sorting strategies without changing the original class. You will sort the same object by different attributes, which is the approach most professional Java applications use.
