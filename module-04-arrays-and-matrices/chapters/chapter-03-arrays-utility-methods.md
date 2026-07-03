# Chapter 3 — Arrays Utility Methods 🧰

## Overview

Until now, you’ve been manually working with arrays:

* looping
* calculating values
* searching
* comparing logic step by step

Java also provides a powerful helper class called:

```java
java.util.Arrays
```

It contains ready-made methods that make array operations **faster, simpler, and less error-prone**.

---

# 📦 Importing Arrays Utility

Before using it:

```java id="import_arrays"
import java.util.Arrays;
```

---

# 🔹 Arrays.toString()

Used to print arrays properly.

### ❌ Without it:

```java id="print_array_wrong"
int[] numbers = {10, 20, 30};

System.out.println(numbers);
```

Output will look like memory reference (not useful).

---

### ✅ With toString():

```java id="print_array_correct"
int[] numbers = {10, 20, 30};

System.out.println(Arrays.toString(numbers));
```

Output:

```
[10, 20, 30]
```

---

# 🔹 Arrays.sort()

Sorts an array in ascending order.

```java id="sort_array"
int[] numbers = {40, 10, 30, 20};

Arrays.sort(numbers);

System.out.println(Arrays.toString(numbers));
```

Output:

```
[10, 20, 30, 40]
```

---

# 🔹 Arrays.binarySearch()

Searches for an element (ONLY works on sorted arrays).

```java id="binary_search"
int[] numbers = {10, 20, 30, 40};

int index = Arrays.binarySearch(numbers, 30);

System.out.println("Index: " + index);
```

Output:

```
Index: 2
```

### ⚠️ Important:

* Array must be sorted
* If not found → returns negative value

---

# 🔹 Arrays.fill()

Fills all positions with the same value.

```java id="fill_array"
int[] numbers = new int[5];

Arrays.fill(numbers, 7);

System.out.println(Arrays.toString(numbers));
```

Output:

```
[7, 7, 7, 7, 7]
```

---

# 🔹 Arrays.copyOf()

Creates a new array with copied values.

```java id="copy_array"
int[] numbers = {10, 20, 30};

int[] copy = Arrays.copyOf(numbers, numbers.length);

System.out.println(Arrays.toString(copy));
```

---

# 🔹 Arrays.equals()

Compares two arrays.

```java id="equals_array"
int[] a = {10, 20, 30};
int[] b = {10, 20, 30};

System.out.println(Arrays.equals(a, b)); // true
```

---

# 🔹 Arrays.deepToString()

Used for **multidimensional arrays** (we will expand later).

```java id="deep_to_string"
int[][] matrix = {
    {1, 2},
    {3, 4}
};

System.out.println(Arrays.deepToString(matrix));
```

Output:

```
[[1, 2], [3, 4]]
```

---

# ⚖️ Manual vs Built-in Methods

| Task        | Manual    | Arrays Utility   |
| ----------- | --------- | ---------------- |
| Print array | loop      | `toString()`     |
| Sort        | algorithm | `sort()`         |
| Search      | loop      | `binarySearch()` |
| Copy        | loop      | `copyOf()`       |
| Fill        | loop      | `fill()`         |

---

# 📌 Key Concepts You Learned

You now understand:

* How to use `java.util.Arrays`
* How to sort arrays easily
* How to search efficiently (binary search)
* How to copy and fill arrays
* How to compare arrays properly

This marks a shift from **manual logic → built-in optimization tools**

---

# 🧪 Practice Exercises

## 1. Array Sorting

* Create an array
* Sort manually (bubble-style if you want)
* Then compare with `Arrays.sort()`

## 2. Search Element

* Search a value manually
* Then use `Arrays.binarySearch()`

## 3. Array Copy

* Create an array
* Copy it using `Arrays.copyOf()`
* Modify original and observe difference

---

# ✔️ Next Step

Proceed to **Chapter 4 — Multidimensional Arrays (Matrices)**, where you will learn how to work with grid-based data structures using two-dimensional arrays and nested loops.
