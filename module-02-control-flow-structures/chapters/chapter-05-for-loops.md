# Chapter 05 — For Loops (Java)

## 🎯 Objective

In this chapter, you will learn how to use the **`for` loop** to control repetition when you already know how many times something should run.

We will focus on:

* `for`
* counting patterns
* accumulation logic
* structured repetition

---

## 🧠 Core Concept

A `for` loop is used when you know:

* where to start
* where to stop
* how to increment

---

## 🔧 Structure

```java id="f1k9aa"
for (initialization; condition; update) {
    // repeated code
}
```

### Example:

```java id="f2k9bb"
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

---

## ⚙️ How it works

1. Initialize (`int i = 0`)
2. Check condition (`i < 5`)
3. Execute block
4. Update (`i++`)
5. Repeat

---

## 🧪 Mini Exercise 1 — Print Numbers

### Goal:

Print numbers from 1 to 10.

### Requirement:

* Use `for`
* Start from 1

---

## 🧪 Mini Exercise 2 — Sum of Numbers

### Goal:

Calculate the sum from 1 to N.

### Steps:

1. Ask user for `N`
2. Use `for` loop
3. Accumulate sum

Example:

* N = 5 → 1+2+3+4+5 = 15

---

## 🧠 Challenge (Optional)

### Factorial Preview

Calculate factorial of a number:

Example:

* 5! = 5 × 4 × 3 × 2 × 1

Hint:

* Use multiplication accumulation inside `for`

---

## ⚠️ Common Mistakes

* Off-by-one errors (`<=` vs `<`)
* Forgetting to initialize accumulator
* Using wrong loop direction

---

## 📌 What you should focus on

* Controlled repetition
* Counting patterns
* Building mathematical logic with loops

---

## 🚀 Next Chapter

Try answering them in your own words. then we'll continue to **Chapter 06 — Enhanced For Loop (For-Each)**, where you'll learn how to iterate through collections in a simpler way.
