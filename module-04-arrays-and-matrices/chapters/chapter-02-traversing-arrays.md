# Chapter 2 — Traversing Arrays 🔁

## Overview

Now that you already know how to **create and access arrays**, the next step is learning how to **process data inside them efficiently**.

In real programs, you rarely access just one element.

You usually need to:

* calculate totals
* find maximum/minimum values
* compute averages
* reverse or analyze data

All of this depends on **array traversal**.

---

# 🔁 What is Array Traversal?

Array traversal means **visiting every element of the array**, usually using loops.

There are two main ways:

* `for` loop (most flexible)
* enhanced `for` (cleaner syntax)

---

# 🔹 Using `for` Loop

This is the most common approach when you need the index.

```java id="for_loop_basic"
int[] numbers = {10, 20, 30, 40};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

### Why use it?

* You have access to the index (`i`)
* You can modify elements
* You can control direction or skip items

---

# 🔹 Using Enhanced for (for-each)

Used when you only care about values.

```java id="foreach_basic"
int[] numbers = {10, 20, 30, 40};

for (int num : numbers) {
    System.out.println(num);
}
```

### Limitation:

* No index access
* Cannot easily modify original array

---

# 📊 Common Array Operations

Now let's apply traversal to real problems.

---

# ➕ Sum of Elements

```java id="sum_array"
int[] numbers = {10, 20, 30, 40};

int sum = 0;

for (int i = 0; i < numbers.length; i++) {
    sum += numbers[i];
}

System.out.println("Sum: " + sum);
```

---

# 📈 Average

```java id="average_array"
int[] numbers = {10, 20, 30, 40};

int sum = 0;

for (int num : numbers) {
    sum += num;
}

double average = (double) sum / numbers.length;

System.out.println("Average: " + average);
```

---

# 🔼 Maximum Value

```java id="max_array"
int[] numbers = {10, 20, 30, 40};

int max = numbers[0];

for (int i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
        max = numbers[i];
    }
}

System.out.println("Max: " + max);
```

---

# 🔽 Minimum Value

```java id="min_array"
int[] numbers = {10, 20, 30, 40};

int min = numbers[0];

for (int num : numbers) {
    if (num < min) {
        min = num;
    }
}

System.out.println("Min: " + min);
```

---

# 🔄 Reverse Array (Concept)

We print elements in reverse order:

```java id="reverse_array"
int[] numbers = {10, 20, 30, 40};

for (int i = numbers.length - 1; i >= 0; i--) {
    System.out.println(numbers[i]);
}
```

---

# 📌 Key Concepts You Learned

You should now understand:

* How to iterate through arrays
* Difference between `for` and `for-each`
* How to calculate:

  * sum
  * average
  * maximum
  * minimum
* How to reverse traversal

This is the **core skill for all array problems**.

---

# 🧪 Practice Exercises

Now implement:

## 1. Student Grades (Part 2)

* Store 5 grades
* Calculate:

  * average
  * highest grade
  * lowest grade

## 2. Reverse Array

* Print an array in reverse order

## 3. Statistics

* Given an array:

  * sum
  * average
  * max
  * min

---

# ✔️ Next Step

Proceed to **Chapter 3 — Arrays Utility Methods**, where you will learn how Java provides built-in tools like `Arrays.sort()`, `binarySearch()`, and other powerful utilities to manipulate arrays efficiently.
