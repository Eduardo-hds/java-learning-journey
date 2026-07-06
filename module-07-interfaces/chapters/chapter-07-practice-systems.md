# Chapter 07 — Practice Systems (Guided Exercises)

---

# 🧩 What This Chapter Is About

Now we apply everything you learned:

* Interfaces as contracts
* Multiple implementations
* Runtime polymorphism
* Service layer decoupling

We will build **small systems**, each focusing on one idea.

You will NOT receive full solutions upfront — only structure, direction, and key code pieces when needed.

---

# 🔷 1. Payment System (Core Practice)

## 🎯 Goal

Build a system where different payment methods can be used interchangeably.

---

## 📌 Required Structure

* `PaymentMethod` (interface)
* `CreditCard`
* `PayPal`
* `PIX`
* `PaymentService`

---

## 🧠 What you must implement

### Interface

Define a contract like:

* process payment

---

### Implementations

Each class must:

* implement the interface
* define its own behavior

Example behavior idea:

* CreditCard → “Processing credit card…”
* PIX → “Processing PIX…”

---

### Service

Must:

* accept interface type
* NOT depend on concrete classes

---

## 🔥 Key Challenge

Your service must work like this:

* same method call
* different behaviors depending on object passed

---

# 🔷 2. Notification System

## 🎯 Goal

Send messages using different channels.

---

## 📌 Structure

* `Notification` (interface)
* `EmailNotification`
* `SMSNotification`

---

## 🧠 Requirements

Each implementation should:

* define how message is sent

Service should:

* send notification using interface reference

---

## 💡 Design Focus

This system reinforces:

> “One action → multiple behaviors”

---

# 🔷 3. Animal Behavior System

## 🎯 Goal

Model different animal sounds using interfaces.

---

## 📌 Structure

* `SoundMaker` (interface)
* `Dog`
* `Cat`
* `Cow`

---

## 🧠 Requirements

Each animal:

* implements sound behavior
* produces different output

---

## 💡 Key Idea

Same method → different behavior per class.

---

# 🔷 4. Transport System

## 🎯 Goal

Simulate different transport types.

---

## 📌 Structure

* `Transport` (interface)
* `Car`
* `Bike`
* `Bus`

---

## 🧠 Requirements

Each transport must:

* implement a method like `move()`

---

## 💡 Focus

Think:

> “Same action (move), different execution”

---

# 🔷 5. Service Layer Design (Advanced Practice)

## 🎯 Goal

Introduce abstraction between logic and implementation.

---

## 🧠 Idea

Instead of directly calling classes:

❌ Bad:

```java
new CreditCard().processPayment();
```

✔ Good:

```java
PaymentService uses PaymentMethod
```

---

## 💡 Your task

Design:

* a service that depends only on interfaces
* multiple interchangeable implementations

---

# 🧠 Overall Pattern You Are Practicing

All systems follow:

```text id="pattern1"
Interface → Multiple Implementations → Service → Runtime Selection
```

---

# ⚠️ Important Rules

* NEVER hardcode concrete classes inside service logic
* ALWAYS use interface references
* Focus on flexibility, not complexity
* Keep console output simple

---

# 🎯 What You Should Be Learning Here

By the end of this chapter, you should clearly understand:

* Interfaces remove dependency on concrete classes
* Systems become interchangeable
* Behavior can be swapped at runtime
* Code becomes easier to extend

---

# 🚀 Next Step

Next we move to the final challenge:

> **Chapter 08 — Final Project: Flexible Payment Processing System**

Where you will:

* design a full system
* integrate everything learned
* apply clean architecture thinking
* simulate real-world design

Proceed when ready.
