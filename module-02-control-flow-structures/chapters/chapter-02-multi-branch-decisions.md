# Chapter 02 — Multi-Branch Decisions (Java)

## 🎯 Objective

In this chapter, you will learn how to handle **multiple possible outcomes** using:

* `switch`
* structured menu logic
* cleaner decision-making compared to many `if-else` blocks

---

## 🧠 Core Concept

When you have **many fixed options**, `switch` is often cleaner than `if-else`.

Example:

* Days of the week
* Menu selections
* Fixed categories

---

## 🔧 Switch Structure

```java
switch (value) {
    case 1:
        System.out.println("Option 1");
        break;
    case 2:
        System.out.println("Option 2");
        break;
    default:
        System.out.println("Invalid option");
}
```

---

## ⚙️ Important Rules

* Each `case` must usually end with `break`
* `default` is the fallback option
* Works well with:

  * `int`
  * `char`
  * `String`

---

## 🧪 Mini Exercise 1 — Day of the Week

### Goal:

Create a program that receives a number (1–7) and prints the corresponding day.

### Mapping:

* 1 → Monday
* 2 → Tuesday
* 3 → Wednesday
* 4 → Thursday
* 5 → Friday
* 6 → Saturday
* 7 → Sunday

### Your task:

* Use `switch`
* Handle invalid inputs with `default`

---

## 🧪 Mini Exercise 2 — Simple Calculator Menu

### Goal:

Build a basic calculator using a menu system.

### Menu:

```
1 - Add
2 - Subtract
3 - Multiply
4 - Divide
```

### Requirements:

1. Ask for two numbers
2. Ask for the operation
3. Use `switch` to decide the operation
4. Print the result

---

## 🧠 Challenge (Optional but important)

Improve the calculator:

* Prevent division by zero
* Add a message for invalid option
* Repeat logic using your knowledge from Chapter 01 (optional thinking ahead)

---

## ⚠️ Common Mistakes

* Forgetting `break` → causes fall-through
* Using `switch` when `if` is more appropriate
* Not handling invalid input

---

## 📌 What you should focus on

* Clean menu logic
* Understanding `switch` flow
* Avoiding repeated `if-else` chains

---

## 🚀 When you're done

Try answering them in your own words. then we'll continue to **Chapter 03 — While Loops**, where you'll start controlling repetition and building real interactive programs.
