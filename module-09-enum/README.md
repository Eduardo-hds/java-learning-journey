# Bootcamp Java — Module 09: Enums

## 📌 Module Index (Structure Overview)

This module is divided into the following learning chapters:

### **Chapter 1 — Enum Fundamentals**

* What enums are
* Why they exist
* Problems solved vs constants

### **Chapter 2 — Defining Enums**

* `enum` keyword
* Declaring enum constants
* Basic usage in Java

### **Chapter 3 — Enums in Java (Internal View)**

* Enums as special classes
* Fields, methods, constructors (basic)
* Memory and structure concept

### **Chapter 4 — Enum Utility Methods**

* `values()`
* `valueOf()`
* `ordinal()` and risks

### **Chapter 5 — Enums with Logic**

* Switch with enums
* Behavior per enum constant
* Clean state handling

### **Chapter 6 — Real-World Modeling with Enums**

* Order status system
* Payment types
* Roles and traffic light simulation

### **Chapter 7 — Final Project**

* Console-based Order Management System using enums

---

## 🧠 Final Project Design — Order Management System

### 📦 Structure (mandatory)

```text
src/
 ├── Main.java
 ├── model/
 │    ├── OrderStatus.java (enum)
 │    ├── PaymentType.java (enum)
 │    ├── TrafficLight.java (enum)
 │    ├── Order.java
 │    └── Product.java
 ├── service/
 └── util/
```

---

## 🧩 System Overview

You will build a **console-based Order Management System** that simulates real business logic using enums for state control and type safety.

### Core Flow:

1. Create an order
2. Assign products
3. Set payment type
4. Change order status
5. Display current order state
6. Simulate status transitions using enum logic

---

## 🧠 Enum Design Overview

### `OrderStatus`

Controls lifecycle of an order:

* PENDING
* PROCESSING
* SHIPPED
* DELIVERED
* CANCELLED

👉 Used to enforce valid state transitions

---

### `PaymentType`

Defines how payment is made:

* CREDIT_CARD
* DEBIT_CARD
* PIX
* PAYPAL

👉 Replaces string or int-based payment codes

---

### `TrafficLight` (learning exercise)

* RED
* YELLOW
* GREEN

👉 Used to demonstrate behavior per enum state

---

## 🏗️ Class Design Overview

### `Order`

* id
* product list
* OrderStatus status
* PaymentType paymentType

Methods:

* changeStatus()
* addProduct()
* showDetails()

---

### `Product`

* name
* price

---

## 🔁 Enum Logic Requirement

You MUST use:

* `switch (enum)`
* state transitions (OrderStatus changes)
* at least one behavior inside enum OR switch-based behavior

---

## 🎯 Learning Goals of This Project

* Replace magic strings / numbers with enums
* Improve type safety
* Control valid states explicitly
* Make code more readable and maintainable
* Prevent invalid assignments at compile time

---

## 💡 Why Enums Improve Design (Critical Concept)

### ❌ Without enums:

```java
String status = "shipped";
```

Problems:

* Typos break logic ("shiped", "SHIPPEDD")
* No compile-time safety
* Hard to refactor
* No controlled set of values

---

### ✅ With enums:

```java
OrderStatus status = OrderStatus.SHIPPED;
```

Benefits:

* Compile-time validation
* Limited valid values
* Cleaner switch logic
* Self-documenting code
* Easier maintenance

---

## 🚀 Next Step

We will begin with:

# Chapter 1 — Enum Fundamentals

We will cover:

* What enums are (conceptually)
* Why they exist
* How they compare to constants (`static final`)
* First real examples in Java
