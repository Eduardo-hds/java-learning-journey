# Chapter 1 — Introduction to Arrays 📦

## Overview

Until now, you’ve been working mainly with single variables like `int`, `double`, and `String`.

The problem is simple:
What if you need to store **multiple values of the same type**?

For example:

* Grades of a student
* Ages of a group
* Prices of products

Creating one variable for each value would be inefficient and impossible at scale.

That’s where **arrays** come in.

---

## What is an Array?

An **array** is a fixed-size structure that stores multiple values of the same type in a single variable.

Instead of:

```java
int grade1 = 80;
int grade2 = 90;
int grade3 = 70;
```

You use:

```java
int[] grades = {80, 90, 70};
```

Now all values are grouped together in one structure.

---

## Declaring Arrays

You can declare an array in two ways:

```java
int[] numbers;
```

or

```java
int numbers[];
```

Both are valid, but the first style is preferred in Java.

---

## Creating Arrays

Declaring alone does not allocate memory.

You must create the array:

```java
int[] numbers = new int[5];
```

This creates an array that can store 5 integers.

---

## Initializing Arrays

### Option 1 — Manual assignment:

```java
int[] numbers = new int[3];

numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
```

---

### Option 2 — Direct initialization:

```java
int[] numbers = {10, 20, 30};
```

---

## Accessing Elements

Array positions start at **0**.

```java
int[] numbers = {10, 20, 30};

System.out.println(numbers[0]); // 10
System.out.println(numbers[1]); // 20
System.out.println(numbers[2]); // 30
```

---

## Updating Values

You can change values using their index:

```java
int[] numbers = {10, 20, 30};

numbers[1] = 99;

System.out.println(numbers[1]); // 99
```

---

## Array Length

Every array has a fixed size:

```java
int[] numbers = {10, 20, 30, 40};

System.out.println(numbers.length); // 4
```

Important:

* `length` is NOT a method
* It is a property

---

## Default Values

When you create an array without initializing values, Java assigns defaults:

| Type    | Default Value |
| ------- | ------------- |
| int     | 0             |
| double  | 0.0           |
| boolean | false         |
| String  | null          |

Example:

```java
int[] numbers = new int[3];

System.out.println(numbers[0]); // 0
```

---

## Array Traversal (Introduction)

To process all elements, we use loops.

### Using `for`:

```java
int[] numbers = {10, 20, 30};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

---

### Using enhanced for (for-each):

```java
int[] numbers = {10, 20, 30};

for (int num : numbers) {
    System.out.println(num);
}
```

---

## Key Idea of This Chapter

You should now understand:

* What arrays are
* How to declare and create them
* How to access and update values
* How indexing works
* How to loop through arrays

This is the foundation for everything that comes next.

---

# 🧪 Practice (Student Grades — Part 1)

Create a program that:

* Stores 5 student grades in an array
* Prints all grades using a loop

No calculations yet — just storage and output.

---

# ✔️ Next Step

Proceed to **Chapter 2 — Traversing Arrays**, where you will learn how to process arrays properly using loops to calculate values like sum, average, maximum, and minimum.
