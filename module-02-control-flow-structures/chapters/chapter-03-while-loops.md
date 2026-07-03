# Chapter 03 — While Loops (Java)

## 🎯 Objective

In this chapter, you will learn how to repeat code **while a condition is true** using:

* `while`
* repetition logic
* user-driven loops
* sentinel values (stop conditions)

---

## 🧠 Core Concept

A `while` loop keeps running **as long as the condition is true**.

```java id="w1q9lp"
while (condition) {
    // repeated code
}
```

⚠️ If the condition never becomes false → infinite loop.

---

## 🔧 Basic Example

```java id="k2x9aa"
int i = 0;

while (i < 5) {
    System.out.println(i);
    i++;
}
```

---

## ⚙️ Key Idea: Control the Loop

You must always control:

* When it starts
* When it stops
* How it changes each iteration

---

## 🧪 Mini Exercise 1 — Sum Until Zero

### Goal:

Keep asking the user for numbers and sum them until they type `0`.

### Rules:

* If user enters `0`, stop loop
* Print final sum

### What you practice:

* sentinel value (`0`)
* accumulation variable
* loop control

---

## 🧪 Mini Exercise 2 — Password Retry System

### Goal:

Allow the user to try entering a password until it is correct.

### Rules:

* Correct password = `"java123"`
* Keep asking while incorrect
* Stop when correct

### What you practice:

* string comparison (`.equals`)
* loop validation
* user repetition

---

## 🧠 Challenge (Optional)

Upgrade the password system:

* Limit attempts to 3
* After 3 wrong attempts → lock system

---

## ⚠️ Common Mistakes

* Forgetting to update loop variable → infinite loop
* Using `==` for strings instead of `.equals()`
* Not defining a clear stop condition

---

## 📌 What you should focus on

* Controlling repetition safely
* Using loops for user interaction
* Understanding infinite loop risks

---

## 🚀 When you're done

When ready to proceed after this chapter, go to the next chapter.
