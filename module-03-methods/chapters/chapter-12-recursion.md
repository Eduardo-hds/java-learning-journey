# Chapter 12 — Recursion

## Overview

Throughout this module, every method you've written has been called by **another method**.

For example:

```text
main()
    ↓
showMenu()
    ↓
printResult()
```

But Java allows something unusual:

A method can call **itself**.

This technique is called **recursion**.

At first, recursion may seem strange—even impossible—but once you understand its execution flow, it becomes a powerful tool for solving certain types of problems.

For this chapter, the goal is **understanding recursion**, not replacing loops everywhere. In real-world Java applications, loops are often simpler and more efficient for many tasks.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what recursion is.
* Identify the base case.
* Identify the recursive case.
* Trace the execution of a recursive method.
* Compare recursive and iterative solutions.
* Know when recursion should and should not be used.

---

# What Is Recursion?

A recursive method is simply:

> **A method that calls itself.**

Example:

```java
public static void countdown(int number) {

    System.out.println(number);

    countdown(number - 1);

}
```

At first glance this looks fine...

But what happens?

```
3
2
1
0
-1
-2
-3
...
```

It never stops.

Eventually, Java runs out of stack memory and throws:

```text
StackOverflowError
```

---

# The Two Parts of Every Recursive Method

Every recursive method must have **two essential parts**.

## 1. Base Case

The condition that stops the recursion.

Example:

```java
if (number == 0) {
    return;
}
```

Without a base case, recursion never ends.

---

## 2. Recursive Case

The part where the method calls itself.

Example:

```java
countdown(number - 1);
```

Each recursive call should move the problem closer to the base case.

---

# A Correct Recursive Countdown

```java
public static void countdown(int number) {

    if (number == 0) {
        System.out.println(0);
        return;
    }

    System.out.println(number);

    countdown(number - 1);

}
```

Calling:

```java
countdown(5);
```

Output:

```text
5
4
3
2
1
0
```

---

# Understanding the Execution

Calling:

```java
countdown(3);
```

Execution:

```text
countdown(3)

↓

Print 3

↓

countdown(2)

↓

Print 2

↓

countdown(1)

↓

Print 1

↓

countdown(0)

↓

Print 0

↓

Return

↓

Return

↓

Return

↓

Finished
```

Notice that each call waits for the next one to finish before completing.

---

# Recursive Factorial

Let's rewrite the factorial algorithm using recursion.

Recall the mathematical definition:

```text
5! = 5 × 4!
```

```text
4! = 4 × 3!
```

```text
3! = 3 × 2!
```

```text
2! = 2 × 1!
```

```text
1! = 1
```

This naturally fits recursion.

---

## Recursive Implementation

```java
public static long factorial(int number) {

    if (number <= 1) {
        return 1;
    }

    return number * factorial(number - 1);

}
```

Calling:

```java
System.out.println(factorial(5));
```

Output:

```text
120
```

---

# Step-by-Step Execution

```
factorial(5)

↓

5 × factorial(4)

↓

5 × (4 × factorial(3))

↓

5 × (4 × (3 × factorial(2)))

↓

5 × (4 × (3 × (2 × factorial(1))))

↓

5 × (4 × (3 × (2 × 1)))

↓

120
```

This illustrates why recursion is often described as **breaking a problem into smaller versions of itself**.

---

# Comparing Iteration and Recursion

## Iterative Version

```java
public static long factorial(int number) {

    long result = 1;

    for (int i = 2; i <= number; i++) {
        result *= i;
    }

    return result;

}
```

---

## Recursive Version

```java
public static long factorial(int number) {

    if (number <= 1) {
        return 1;
    }

    return number * factorial(number - 1);

}
```

Both return the same result.

The difference is **how** they solve the problem.

---

# Which One Is Better?

For factorial, the iterative solution is generally preferred.

Why?

* Simpler execution.
* Faster.
* Uses less memory.
* No risk of `StackOverflowError` for large values.

The recursive version is valuable because it teaches an important programming technique, not because it is always the most practical solution.

---

# When Recursion Is a Good Choice

Recursion is excellent for naturally recursive problems, such as:

* Tree traversal.
* Folder/directory exploration.
* Graph algorithms.
* Divide-and-conquer algorithms.
* Some mathematical definitions.

You'll encounter these topics later in your programming journey.

---

# When to Avoid Recursion

Avoid recursion when:

* A simple loop is easier to understand.
* The recursion depth can become very large.
* Performance and memory usage are critical.
* There's no natural recursive structure.

A good programmer chooses the simplest correct solution.

---

# Exercise 7 — Recursive Factorial

Implement:

```java
public static long factorialRecursive(int number)
```

Requirements:

* Use recursion.
* Include a base case.
* Return `-1` for negative numbers.
* Return `1` for `0!` and `1!`.

One possible implementation:

```java
public static long factorialRecursive(int number) {

    if (number < 0) {
        return -1;
    }

    if (number <= 1) {
        return 1;
    }

    return number * factorialRecursive(number - 1);

}
```

---

# Compare Both Solutions

Create both methods:

```java
factorialIterative(int number)
```

and

```java
factorialRecursive(int number)
```

Print:

```text
Factorial Comparison

Input: 6

Iterative: 720

Recursive: 720
```

Observe that the results are identical.

Only the implementation differs.

---

# Common Beginner Mistakes

### Forgetting the Base Case

```java
public static void example(int n) {
    example(n - 1);
}
```

Infinite recursion.

Eventually:

```text
StackOverflowError
```

---

### Not Moving Toward the Base Case

Incorrect:

```java
factorial(number);
```

The parameter never changes.

The recursion never ends.

Always move closer to the stopping condition.

---

### Using Recursion for Everything

Not every loop should become recursion.

Sometimes:

```java
for (...)
```

is simply the better solution.

---

# Best Practices

✔ Every recursive method must have a clear base case.

✔ Every recursive call should move closer to that base case.

✔ Prefer iteration when it's simpler and more efficient.

✔ Use recursion when it naturally models the problem.

✔ Always consider readability before cleverness.

---

# Summary

In this chapter, you learned:

* What recursion is.
* The difference between a base case and a recursive case.
* How recursive methods execute.
* How to implement factorial recursively.
* The differences between iterative and recursive solutions.
* When recursion is appropriate and when loops are usually the better choice.
* Why understanding recursion is important even if you don't use it every day.

---

# Module 03 Completed 🎉

Congratulations!

You have successfully completed all the lessons in **Module 03 — Methods**.

Throughout this module, you learned how to:

- Create and invoke methods.
- Pass parameters and arguments.
- Return values.
- Understand variable scope.
- Organize code into small, reusable methods.
- Use method overloading.
- Work with variable arguments (varargs).
- Implement recursive methods.
- Build cleaner and more modular console applications.

These concepts are fundamental to writing organized and maintainable Java programs.

---

## Next Step

Before moving on to **Module 04**, complete the **Final Project — Utility Toolkit**.

This project is designed to reinforce everything you've learned in this module by combining all concepts into a single console application.

Take your time to design the program carefully, keep your methods focused on a single responsibility, and avoid duplicating code.

The goal is not only to make the application work, but also to practice writing clean, reusable, and well-structured code.

Once the Final Project is complete, you'll be ready to begin **Module 04**, where you'll take the next big step in your Java journey by learning **Object-Oriented Programming**, including classes, objects, and encapsulation.