# Chapter 4 — Multidimensional Arrays (Matrices) 🧮

## Overview

Until now, you’ve been working with **one-dimensional arrays**, which are like a simple list:

```
[10, 20, 30]
```

But real-world data is often structured in **tables**, such as:

* student grades per exam
* spreadsheet data
* game boards (like chess)
* images (pixels)

For that, we use **multidimensional arrays**, especially **2D arrays (matrices)**.

---

# 🧱 What is a Matrix?

A matrix is an array of arrays.

Example:

```
1  2  3
4  5  6
```

In Java:

```java id="matrix_basic"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

* Rows → horizontal
* Columns → vertical

---

# 📦 Declaring a Matrix

```java id="matrix_declare"
int[][] matrix;
```

---

# 🏗️ Creating a Matrix

```java id="matrix_create"
int[][] matrix = new int[2][3];
```

Meaning:

* 2 rows
* 3 columns

---

# ✍️ Initializing a Matrix

### Option 1 — Manual assignment:

```java id="matrix_manual"
int[][] matrix = new int[2][3];

matrix[0][0] = 1;
matrix[0][1] = 2;
matrix[0][2] = 3;

matrix[1][0] = 4;
matrix[1][1] = 5;
matrix[1][2] = 6;
```

---

### Option 2 — Direct initialization:

```java id="matrix_direct"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

---

# 🔍 Accessing Elements

You use two indexes:

```java id="matrix_access"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[0][0]); // 1
System.out.println(matrix[1][2]); // 6
```

---

# 🔁 Traversing a Matrix (Nested Loops)

To go through all elements, we use **two loops**:

```java id="matrix_traversal"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

---

# 📌 Key Idea:

* `i` → rows
* `j` → columns

---

# ➕ Row Sum Example

```java id="row_sum"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

for (int i = 0; i < matrix.length; i++) {
    int sum = 0;

    for (int j = 0; j < matrix[i].length; j++) {
        sum += matrix[i][j];
    }

    System.out.println("Row " + i + " sum: " + sum);
}
```

---

# ➕ Column Sum Example

```java id="column_sum"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

for (int j = 0; j < matrix[0].length; j++) {
    int sum = 0;

    for (int i = 0; i < matrix.length; i++) {
        sum += matrix[i][j];
    }

    System.out.println("Column " + j + " sum: " + sum);
}
```

---

# 📌 Key Concepts You Learned

You now understand:

* What a matrix is
* How to declare and create 2D arrays
* How to access elements using `[row][column]`
* How nested loops work
* How to calculate row and column operations

This is the foundation for structured data processing.

---

# 🧪 Practice Exercises

## 1. Matrix Input/Output

* Create a 2x3 matrix
* Fill it manually
* Print using nested loops

## 2. Row Sum

* Calculate sum of each row

## 3. Column Sum

* Calculate sum of each column

---

# ✔️ Next Step

Proceed to **Chapter 5 — Matrix Operations**, where you will learn how to work with diagonals and transpose matrices, unlocking more advanced matrix manipulation techniques.
