# Chapter 08 — Final Project: Flexible Payment Processing System

---

# 🧩 Project Goal

You will build a **console-based payment system** where:

> The system can process payments using different methods without changing the core service logic.

This is a direct real-world simulation of how payment gateways work.

---

# 🔷 Core Requirement

You must implement a system that:

* Uses **at least 1 interface**
* Has **at least 3 implementations**
* Uses **interface references (polymorphism)**
* Demonstrates **runtime behavior switching**
* Has **clean package separation**
* Separates **model and service layers**

---

# 📦 Required Structure

```text id="final_structure"
src/
 ├── Main.java
 ├── model/
 │    ├── PaymentMethod.java
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

# 🔷 1. Interface Design

## 🎯 PaymentMethod

You must define a contract that represents:

> “Any payment method must be able to process a payment.”

### Requirements:

* One method only (keep it simple)
* Must accept a value (double or similar)

---

# 🔷 2. Implementations

You must create at least 3:

* CreditCard
* PayPal
* PIX

---

## 🧠 Behavior Rule

Each implementation must:

* print a different message
* simulate different payment behavior

Example idea (not full solution):

* CreditCard → “Charging credit card…”
* PayPal → “Processing PayPal account…”
* PIX → “Sending PIX transfer…”

---

# 🔷 3. Service Layer

## 🎯 PaymentService

This class must:

* NOT depend on concrete classes
* ONLY depend on `PaymentMethod`

---

## 🧠 Core Method

You should design something like:

* process payment using interface reference

---

## 💡 Critical Rule

❌ DO NOT do:

```java
new CreditCard()
```

inside the service.

✔ DO:

```java
PaymentMethod method
```

---

# 🔷 4. Main Class (User Flow Simulation)

## 🎯 Goal

Simulate user selecting payment methods.

---

## 🧠 Expected Flow

1. User chooses payment method
2. System creates correct implementation
3. System passes it to service
4. Service processes payment
5. Behavior changes depending on selection

---

## 🔁 Example Runtime Behavior

```text id="runtime_flow"
User selects: PIX
→ PIX object created
→ PaymentService processes it
→ Output: PIX payment message

User selects: PayPal
→ PayPal object created
→ Same service used
→ Different output
```

---

# 🔷 5. Key Design Rule

Your system must demonstrate:

> One service → multiple behaviors → runtime switching

---

# 🧠 What You Are Being Tested On

This project checks if you understand:

* Interface abstraction
* Loose coupling
* Runtime polymorphism
* Clean architecture separation

---

# ❌ Common Mistakes (Avoid These)

* Using `if-else` for payment types
* Hardcoding concrete classes inside service
* Mixing logic inside Main
* Not using interface references

---

# 🌍 Real-World Connection

This is how real systems work:

* Stripe / PayPal integrations
* Banking systems
* Checkout APIs

They all follow:

> “Same interface, different providers”

---

# 🎯 Final Concept Summary

If you understand this project, you understand:

> Interfaces are not about code — they are about architecture flexibility.
