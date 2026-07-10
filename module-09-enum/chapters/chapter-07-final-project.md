# Chapter 7 — Final Project: Order Management System

Congratulations! In this final chapter, you'll combine everything you've learned about enums into a small but realistic console application.

> **Important:** As required by the bootcamp methodology, I will **guide** you through the project step by step. I will **not** provide the complete solution upfront.

---

# 🎯 Project Goal

Build a console-based **Order Management System** that uses enums to model business rules safely and clearly.

By the end, your project will demonstrate:

* ✅ Multiple enums
* ✅ Enums inside domain classes
* ✅ Switch expressions/statements
* ✅ State transitions
* ✅ Good package organization
* ✅ Clean OOP design

---

# 📁 Step 1 — Create the Project Structure

Create the following folders and files:

```text
src/
 ├── Main.java
 ├── model/
 │    ├── OrderStatus.java
 │    ├── PaymentType.java
 │    ├── Product.java
 │    └── Order.java
 ├── service/
 └── util/
```

At this stage:

* `service/` and `util/` may remain empty.
* The focus is on organizing your project properly.

---

# 📋 Step 2 — Create the Enums

## OrderStatus

Create an enum with exactly these constants:

```text
PENDING
PROCESSING
SHIPPED
DELIVERED
CANCELLED
```

---

## PaymentType

Create another enum with:

```text
CREDIT_CARD
DEBIT_CARD
PIX
PAYPAL
```

Do **not** add methods yet.

---

# 📦 Step 3 — Create the Product Class

Create a simple `Product` class.

Suggested fields:

```text
name
price
```

Suggested constructor:

```text
Product(String name, double price)
```

Suggested methods:

* getters
* `toString()`

Nothing more is needed.

---

# 📦 Step 4 — Create the Order Class

Create an `Order` class.

Suggested fields:

```text
id
Product product
OrderStatus status
PaymentType paymentType
```

In the constructor:

* initialize the `status` as `PENDING`

This models a common real-world rule:

> Every newly created order starts in the **PENDING** state.

---

# 🔄 Step 5 — Add State Transition

Create a method similar to:

```text
changeStatus(...)
```

It should receive an `OrderStatus`.

Example usage:

```java
order.changeStatus(OrderStatus.PROCESSING);
order.changeStatus(OrderStatus.SHIPPED);
```

Notice how impossible it is to accidentally pass an invalid value.

This is one of the biggest advantages of enums.

---

# 💳 Step 6 — Add Payment Type

Create a method like:

```text
setPaymentType(...)
```

Accept only:

```java
PaymentType
```

Example:

```java
order.setPaymentType(PaymentType.PIX);
```

Again, Java guarantees that only valid payment methods can be assigned.

---

# 🔀 Step 7 — Use Switch

Create a method that prints a message depending on the current order status.

For example:

```text
PENDING      -> Waiting for processing...
PROCESSING   -> Preparing your order...
SHIPPED      -> Order is on the way...
DELIVERED    -> Order delivered.
CANCELLED    -> Order cancelled.
```

Use a `switch` with the enum.

This is much cleaner than comparing strings.

---

# 🖥️ Step 8 — Test Everything in Main

Create an order.

Example flow:

```text
Create Product

↓

Create Order

↓

Set Payment Type

↓

Show Current Status

↓

Change Status

↓

Show Current Status Again

↓

Repeat Until Delivered
```

Expected console behavior:

```text
Order #1 created

Status:
PENDING

Payment:
PIX

Changing status...

PROCESSING

Changing status...

SHIPPED

Changing status...

DELIVERED
```

The exact formatting is up to you.

---

# ⭐ Bonus Challenge (Recommended)

Add a method that displays information about the order using a `switch` on the payment type.

For example:

```text
PIX
→ Instant payment

CREDIT_CARD
→ Processing card payment

PAYPAL
→ Redirecting to PayPal
```

This reinforces that enums are excellent for expressing business rules.

---

# 🧠 What You Learned in This Module

You can now confidently:

* Define enums with the `enum` keyword
* Replace fragile strings and integer constants
* Use enums inside classes
* Iterate with `values()`
* Convert text with `valueOf()`
* Understand why `ordinal()` should rarely be used
* Write `switch` statements with enums
* Model business concepts such as status, payment types, and user roles
* Build safer and more maintainable applications

---

# 🏆 Module Completion Report

## Module 09 — Enums

**Status:** ✅ Completed

### Topics Covered

* ✅ Enum fundamentals
* ✅ Why enums exist
* ✅ `enum` keyword
* ✅ Enum constants
* ✅ Enums as special classes
* ✅ Constructors and methods (conceptual understanding)
* ✅ `values()`
* ✅ `valueOf()`
* ✅ `ordinal()` and its risks
* ✅ Switch with enums
* ✅ Enums with business logic
* ✅ Best practices
* ✅ Real-world domain modeling

### Practical Exercises Completed

* ✅ Order Status System
* ✅ Payment Types
* ✅ Traffic Light Simulation
* ✅ User Role System
* ✅ Switch with Enums
* ✅ Enum-based Order System

### Final Project

**Order Management System**

Features:

* ✅ Multiple enums
* ✅ Domain classes using enums
* ✅ State transitions
* ✅ Switch-based behavior
* ✅ Console application
* ✅ Organized package structure

---

# 🚀 Next Module

The next logical step is **Module 10 — Exception Handling**.

You'll learn:

* What exceptions are
* Checked vs unchecked exceptions
* `try`, `catch`, `finally`
* `throw` and `throws`
* Creating custom exceptions
* Writing more robust and fault-tolerant Java applications

This module will build directly on everything you've learned so far, allowing your programs to handle unexpected situations gracefully.
