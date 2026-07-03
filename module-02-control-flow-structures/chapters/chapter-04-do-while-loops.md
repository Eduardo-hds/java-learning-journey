
# Chapter 04 — Do While Loops (Java)

## 🎯 Objective

In this chapter, you will learn how to use a loop that **always runs at least once**, using:

* `do while`
* menu-based systems
* input validation
* controlled repetition

---

## 🧠 Core Concept

Unlike `while`, a `do while` loop:

👉 Executes the block first
👉 Checks the condition after

---

## 🔧 Structure

```java id="d1q8aa"
do {
    // code runs at least once
} while (condition);
```

---

## ⚙️ Key Difference

| Loop     | When condition is checked |
| -------- | ------------------------- |
| while    | before running            |
| do while | after running             |

---

## 🧪 Example — Basic Menu Loop

```java id="m9x2pl"
int option;

do {
    System.out.println("1 - Say Hello");
    System.out.println("2 - Exit");
    option = scanner.nextInt();

    if (option == 1) {
        System.out.println("Hello!");
    }

} while (option != 2);
```

---

## 🧪 Mini Exercise 1 — Menu System

### Goal:

Create a menu that runs at least once:

### Menu:

* 1 → Print "Start"
* 2 → Print "Settings"
* 3 → Exit

### Rules:

* Must use `do while`
* Loop continues until user selects `3`

---

## 🧪 Mini Exercise 2 — Input Validation

### Goal:

Force the user to enter a valid number between 1 and 5.

### Rules:

* Keep asking while input is invalid
* Accept only values from 1 to 5

### What you practice:

* validation loops
* condition checking
* user input control

---

## 🧠 Challenge (Optional)

Upgrade the menu system:

* Add a counter of how many actions were performed
* Show the counter when exiting

---

## ⚠️ Common Mistakes

* Forgetting the semicolon after `while(condition);`
* Using `while` instead of `do while` for menus
* Not ensuring loop exit condition works

---

## 📌 What you should focus on

* Guaranteeing at least one execution
* Building menu-driven programs
* Validating user input properly

---

## 🚀 Next Chapter

Try answering them in your own words. then we'll continue to **Chapter 05 — For Loops**, where you'll learn how to control repetition with precise counters and build structured iterations.
