# Chapter 01 — Conditional Logic Basics (Java)

## 🎯 Objective

In this chapter, you will learn how to make a Java program **choose different paths based on conditions** using:

* `if`
* `else`
* boolean expressions
* simple comparisons

This is the foundation of all decision-making in programming.

---

## 🧠 Core Concept

A program normally runs top to bottom.

With `if`, you can change that flow:

```java
if (condition) {
    // runs only if condition is true
}
```

Example idea:

* If a number is greater than 10 → do something
* Otherwise → do something else

---

## 🔧 Basic Structure

### ✅ if

```java
if (x > 10) {
    System.out.println("Greater than 10");
}
```

### ✅ if + else

```java
if (x > 10) {
    System.out.println("Greater than 10");
} else {
    System.out.println("10 or less");
}
```

---

## ⚙️ Comparison Operators

You will use these constantly:

| Operator | Meaning          |
| -------- | ---------------- |
| `==`     | equal            |
| `!=`     | not equal        |
| `>`      | greater than     |
| `<`      | less than        |
| `>=`     | greater or equal |
| `<=`     | less or equal    |

---

## 🧪 Mini Exercise 1 — Even or Odd

### Goal:

Ask the user for a number and determine if it's even or odd.

### Logic hint:

* A number is even if `number % 2 == 0`

### Your task:

Write a program that:

1. Reads an integer
2. Checks if it's even or odd
3. Prints the result

---

## 🧪 Mini Exercise 2 — Positive, Negative or Zero

### Goal:

Classify a number.

### Rules:

* `> 0` → Positive
* `< 0` → Negative
* `== 0` → Zero

### Your task:

Write a program that:

1. Reads an integer
2. Uses `if / else if / else`
3. Prints the classification

---

## 🧠 Challenge (Optional but recommended)

Combine both ideas:

👉 Ask for a number and print:

* Even or Odd
* And also Positive / Negative / Zero

Example output:

```
Number: -4
Even
Negative
```

---

## ⚠️ Common Mistakes

* Using `=` instead of `==`
* Forgetting `{ }` blocks
* Not covering all conditions in `if / else if / else`

---

## 📌 What you should focus on

* Understanding condition flow
* Writing clean boolean expressions
* Avoiding duplicated or unnecessary conditions

---

## 🚀 When you're done

When ready to proceed after this chapter, go to the next chapter.
