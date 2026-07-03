# Chapter 5 — Matrix Operations 🧮✨

## Overview

Now you already know:

* how to create matrices
* how to access elements
* how to traverse using nested loops

In this chapter, we go one level deeper and learn **structured matrix analysis**, which is very common in programming problems.

You will learn how to work with:

* main diagonal
* secondary diagonal
* transpose of a matrix

---

# 📐 Matrix Recap

Example matrix:

```java id="matrix_example"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

Visual:

```
1  2  3
4  5  6
7  8  9
```

---

# 🔵 Main Diagonal

The **main diagonal** goes from top-left to bottom-right:

```
1 → 5 → 9
```

Rule:

* row index == column index

```java id="main_diagonal"
for (int i = 0; i < matrix.length; i++) {
    System.out.println(matrix[i][i]);
}
```

---

# 🟣 Secondary Diagonal

The **secondary diagonal** goes from top-right to bottom-left:

```
3 → 5 → 1
```

Rule:

* column = (size - 1 - row)

```java id="secondary_diagonal"
for (int i = 0; i < matrix.length; i++) {
    System.out.println(matrix[i][matrix.length - 1 - i]);
}
```

---

# 🔄 Matrix Transpose

Transpose means:

* rows become columns
* columns become rows

Example:

```
Original:
1 2 3
4 5 6

Transposed:
1 4
2 5
3 6
```

---

## Code:

```java id="transpose_matrix"
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

int rows = matrix.length;
int cols = matrix[0].length;

int[][] transpose = new int[cols][rows];

for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
        transpose[j][i] = matrix[i][j];
    }
}
```

---

## Print Transposed Matrix:

```java id="print_transpose"
for (int i = 0; i < transpose.length; i++) {
    for (int j = 0; j < transpose[i].length; j++) {
        System.out.print(transpose[i][j] + " ");
    }
    System.out.println();
}
```

---

# 📌 Key Concepts You Learned

You now understand:

* Main diagonal logic
* Secondary diagonal logic
* Matrix transpose
* How to restructure matrix data

These are core patterns used in:

* image processing
* game boards
* data analysis
* algorithm challenges

---

# 🧪 Final Practice (Matrix Challenge)

Create a program that:

1. Defines a 3x3 matrix
2. Prints:

   * main diagonal
   * secondary diagonal
3. Creates and prints the transpose

---

# 🎓 Module 04 Completion Task — Final Project

Now you will build the:

## 🧑‍🎓 Student Grade Management System

Using arrays and matrices, your system must:

### 📌 Features:

* Store student grades in arrays
* Calculate:

  * average per student
  * class average
  * highest and lowest grades
* Search for specific grades
* Display formatted reports
* Represent data in a matrix:

  * rows = students
  * columns = exams

### 📊 Matrix operations:

* row sum → student total score
* column sum → exam performance

---

# ✔️ Next Step

You have completed all content of **Module 04 — Arrays & Matrices**.

Proceed to the final step:
👉 **Build the Final Project (Student Grade Management System)** using everything you learned in this module.
