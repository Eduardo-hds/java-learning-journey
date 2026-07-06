# Chapter 6 — Guided Practice Systems (Step-by-Step Build)

---

# 🧠 1. How This Chapter Works

From now on, we move from theory → **structured practice**.

Important rule:

> You will NOT get full solutions upfront.

Instead:

* We build step by step
* You complete parts mentally or in code
* I guide and correct structure/design

---

# 🧩 System 1 — Animal Hierarchy

## 🎯 Goal

Model:

* Common animal behavior
* Forced implementation per animal type

---

# 🏗️ Step 1 — Abstract Base Class

We start with the base structure.

### Think:

All animals:

* have a name
* can eat (shared behavior)
* make sound (different per animal)

---

## 🧪 Your Task (Step 1)

Complete this mentally:

```java id="a1a1a1"
abstract class Animal {

    String name;

    void eat() {
        System.out.println(name + " is eating");
    }

    abstract void makeSound();
}
```

---

# 🐶 Step 2 — Dog Class

Now we specialize:

### Dog rules:

* Must implement `makeSound`
* Should say "Bark"

---

## 🧪 Your Task (Step 2)

Try writing this:

```java id="b2b2b2"
class Dog extends Animal {

    // implement makeSound()
}
```

---

# 🐱 Step 3 — Cat Class

### Cat rules:

* Must implement `makeSound`
* Should say "Meow"

Same structure as Dog.

---

# 🔥 Key Learning in This System

You are learning:

✔ Shared logic (eat)
✔ Forced behavior (makeSound)
✔ Hierarchical modeling

---

# 🧩 System 2 — Employee System

## 🎯 Goal

Model a real company structure.

---

### Base Rules:

All employees:

* have name
* can clock in (shared)
* must work (different per role)

---

## Abstract Class Idea:

```java id="c3c3c3"
abstract class Employee {

    String name;

    void clockIn() {
        System.out.println(name + " clocked in");
    }

    abstract void work();
}
```

---

## 🧪 Your Task

Create:

* Developer → "writes code"
* Manager → "manages team"

---

# 🧩 System 3 — Shape System

## 🎯 Goal

Force mathematical structure.

---

### Rule:

All shapes MUST:

* calculate area

But each shape differs.

---

## Abstract Class Idea:

```java id="d4d4d4"
abstract class Shape {
    abstract double area();
}
```

---

## 🧪 Your Task

Implement:

* Circle
* Rectangle

---

# 🧩 System 4 — Banking System

## 🎯 Goal

Model financial accounts.

---

### Rule:

All accounts:

* have balance
* can deposit (shared logic)
* can withdraw (custom rules)

---

## Abstract Idea:

```java id="e5e5e5"
abstract class Account {

    double balance;

    void deposit(double amount) {
        balance += amount;
    }

    abstract void withdraw(double amount);
}
```

---

## 🧪 Your Task

Implement:

* SavingsAccount (safe withdrawals)
* CheckingAccount (flexible withdrawals)

---

# 🧠 5. What You Are Learning Here

Across all systems, you are practicing:

### ✔ Partial abstraction

### ✔ Real-world modeling

### ✔ Code reuse vs forced behavior

### ✔ Hierarchy thinking

---

# ⚠️ Important Rule

Do NOT focus only on syntax.

Focus on:

> “Why does this method belong in abstract class vs subclass?”

---

# 🔥 6. Mental Model

Each system follows this pattern:

```
Abstract Class
   ↓
Shared behavior + rules
   ↓
Concrete subclasses
   ↓
Specific implementations
```

---

# ✔️ Your Progress Check

Before we move on, you should be able to answer:

1. Why is eat() NOT abstract in Animal?
2. Why is makeSound() abstract?
3. Why do all employees share clockIn()?
4. Why does withdraw() change per account type?

---

# ▶️ Next Step

Next we move to:

## Chapter 7 — Final Project Design (Abstract System Architecture)

We will design a complete system before coding it.
