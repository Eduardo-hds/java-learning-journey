# Bootcamp Java — Module 07: Interfaces

We will start this module following the established bootcamp structure: index → chapters → core concepts → design overview → final project blueprint.

---

# 📌 Module Index

This module is divided into:

* Chapter 01 — Interface Fundamentals
* Chapter 02 — Defining and Implementing Interfaces
* Chapter 03 — Methods in Interfaces (abstract, default, static)
* Chapter 04 — Polymorphism with Interfaces
* Chapter 05 — Interface vs Inheritance (Design Comparison)
* Chapter 06 — Real-World Design with Interfaces
* Chapter 07 — Practice Systems (Guided Exercises)
* Chapter 08 — Final Project: Flexible Payment Processing System

---

# 📚 Module Overview

In previous modules, you learned how to structure behavior using classes and inheritance.

Now we move into a more important design principle used in professional Java systems:

> **Programming to an interface, not an implementation.**

Interfaces allow us to define **contracts** that classes must follow, without forcing how they should behave internally.

This is the foundation of:

* scalable systems
* loosely coupled architecture
* flexible runtime behavior

---

# 🔷 Interfaces vs Inheritance (Core Conceptual Difference)

Before anything else, this distinction must be clear:

## 🧬 Inheritance (extends)

* Used when there is a **“is-a” relationship**
* Shares **code + behavior**
* Creates a **tight coupling**
* One class can extend only one parent

Example concept:

* Dog **is an** Animal

---

## 📜 Interface (implements)

* Defines a **contract / capability**
* Does NOT provide full implementation (mostly)
* Encourages **loose coupling**
* A class can implement multiple interfaces

Example concept:

* PayPal **is a** PaymentMethod
* CreditCard **is a** PaymentMethod

But also:

* PayPal can also implement LoggingEnabled, SecureTransaction, etc.

---

## ⚖️ Key Difference Summary

| Feature      | Inheritance | Interface  |
| ------------ | ----------- | ---------- |
| Type         | Code reuse  | Contract   |
| Coupling     | Strong      | Weak       |
| Flexibility  | Low         | High       |
| Multiple use | No          | Yes        |
| Purpose      | Hierarchy   | Capability |

---

## 🧠 Why Interfaces Exist

Interfaces were created to solve a major problem:

> “How do we define behavior without locking ourselves into a single implementation?”

Without interfaces:

* systems become rigid
* swapping logic becomes difficult
* testing becomes harder

With interfaces:

* you can replace behavior without changing code structure
* systems become modular
* services become interchangeable

---

# 🧩 Conceptual Architecture of This Module

We will consistently apply this pattern:

```
Interface (Contract)
    ↓
Multiple Implementations
    ↓
Service Layer uses Interface (not concrete class)
    ↓
Runtime decides behavior
```

This is called **dependency on abstraction**.

---

# 🏗️ Final Project Design (DO NOT IMPLEMENT YET)

## 🎯 Project: Flexible Payment Processing System

### Goal:

Build a system where payment behavior can change at runtime without modifying the service logic.

---

## 📦 Structure (as required)

```
src/
 ├── Main.java
 ├── model/
 │    ├── PaymentMethod.java (interface)
 │    ├── CreditCard.java
 │    ├── PayPal.java
 │    ├── PIX.java
 │
 ├── service/
 │    └── PaymentService.java
 │
 └── util/
```

---

## 🔷 Core Design Idea

### 1. Interface Layer

`PaymentMethod`

* defines a method like `processPayment(amount)`

---

### 2. Implementations

Each class represents a different payment behavior:

* CreditCard
* PayPal
* PIX

Each one handles payment differently internally.

---

### 3. Service Layer

`PaymentService`

* does NOT know which payment type is used
* only works with `PaymentMethod`

This is the key design rule:

> Service depends on abstraction, not implementation.

---

### 4. Runtime Behavior

In `Main`:

* user selects payment method
* system assigns correct implementation
* same service processes all types

---

## 🔁 Expected Runtime Concept

```
User chooses PIX
→ PIX object created
→ PaymentService receives PaymentMethod reference
→ processPayment executed dynamically
```

Then:

```
User chooses PayPal
→ same service
→ different behavior automatically
```

---

# 📌 Learning Focus of This Module

During this module, you must internalize:

* Interfaces are NOT about code
* They are about **design**
* They define **flexibility points**
* They enable **runtime substitution**

---

# 🚀 Next Step

We will now begin:

> **Chapter 01 — Interface Fundamentals**

Where we will understand:

* what an interface actually is in Java
* how the JVM treats it conceptually
* and why it changes how we design systems

Proceed when ready.
