# Chapter 06 — Enhanced For Loop (For-Each) (Java)

## 🎯 Objective

In this chapter, you will learn how to iterate over **collections of values (arrays)** using the **enhanced for loop (for-each)**.

We will focus on:

* arrays (basic introduction)
* `for-each` loop
* reading data cleanly
* simplifying iteration

---

## 🧠 Core Concept

The `for-each` loop is used when you want to go through every element of a collection without worrying about indexes.

---

## 🔧 Array Basics

An array is a fixed collection of values:

```java id="a1k9aa"
int[] numbers = {1, 2, 3, 4, 5};
```

---

## 🔧 For-Each Structure

```java id="a2k9bb"
for (type element : array) {
    // use element
}
```

---

## 🧪 Example

```java id="a3k9cc"
int[] numbers = {10, 20, 30};

for (int num : numbers) {
    System.out.println(num);
}
```

---

## ⚙️ How it works

* Takes each element automatically
* No index needed
* Safer and cleaner than `for` in simple cases

---

## 🧪 Mini Exercise 1 — Print Array

### Goal:

Create an array of 5 numbers and print all values.

### Requirement:

* Use `for-each`
* No index usage allowed

---

## 🧪 Mini Exercise 2 — Sum Array Values

### Goal:

Sum all values in an array.

Example:

```text
[2, 4, 6, 8] → 20
```

### Requirement:

* Use `for-each`
* Store result in a variable

---

## 🧠 Challenge (Optional)

Find the largest number in an array.

Hint:

* Start with first element as "max"
* Compare each value

---

## ⚠️ Common Mistakes

* Trying to access index inside for-each
* Forgetting to initialize sum/max variables
* Confusing `for-each` with normal `for`

---

## 📌 What you should focus on

* Clean iteration
* Working with collections (arrays)
* Simplifying loops when possible

---

## 🚀 Next Chapter

Try answering them in your own words. then we'll continue to **Chapter 07 — Flow Control Statements (break, continue, return)**, where you'll learn how to control and interrupt loops and execution flow.
