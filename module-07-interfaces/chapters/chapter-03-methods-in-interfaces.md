# Chapter 03 — Methods in Interfaces (abstract, default, static)

---

# 🧩 What Changes Here?

Until now, you saw interfaces as:

> “Only method contracts with no implementation.”

That was true in older Java versions.

Modern Java changed this idea by allowing **some behavior inside interfaces**.

Now interfaces can contain:

* abstract methods (core contract)
* default methods (shared behavior)
* static methods (utility behavior)

---

# 🔷 1. Abstract Methods (Core Contract)

This is the original and most important part.

```java id="a1b2c3"
public interface PaymentMethod {
    void processPayment(double amount);
}
```

---

## 🧠 What it means

* No implementation
* Must be implemented by classes
* Defines mandatory behavior

---

## ❗ Why it exists

Because every payment method MUST:

* process a payment
* but each one does it differently

So interface forces consistency without forcing implementation.

---

# 🔷 2. Default Methods (Shared Behavior)

Now interfaces can provide a **ready implementation**:

```java id="d4e5f6"
public interface PaymentMethod {

    void processPayment(double amount);

    default void validatePayment() {
        System.out.println("Validating payment before processing...");
    }
}
```

---

## 🧠 What this means

Classes can:

* use this method as-is
* or override it

---

## 💡 Why default methods exist

Before Java 8:

* adding a new method to an interface would break all classes

Now:

* you can add behavior without breaking existing code

---

## 🌍 Real-world idea

Think:

> “All payment methods share a basic validation step.”

So instead of rewriting in every class, interface provides it.

---

## ⚠️ When to use default methods

Use when:

* behavior is common across most implementations
* you want optional override
* you want backward compatibility

Avoid when:

* logic is complex
* behavior varies too much

---

# 🔷 3. Static Methods in Interfaces

Interfaces can also have utility methods:

```java id="g7h8i9"
public interface PaymentMethod {

    void processPayment(double amount);

    static void printSupportedMethods() {
        System.out.println("Supported: CreditCard, PayPal, PIX");
    }
}
```

---

## 🧠 Important rule

Static methods:

* belong to the interface itself
* NOT to implementations

You call them like this:

```java id="j1k2l3"
PaymentMethod.printSupportedMethods();
```

---

## 💡 Why static methods exist here

To group related utility logic inside the interface domain.

Instead of:

* creating a helper class
* or scattering utilities

You keep it logically connected.

---

# ⚙️ Method Comparison

| Type     | Must Implement? | Has Body? | Called By |
| -------- | --------------- | --------- | --------- |
| Abstract | Yes             | No        | Class     |
| Default  | No              | Yes       | Instance  |
| Static   | No              | Yes       | Interface |

---

# 🔁 How It Works Internally

At runtime:

* Abstract methods → resolved by object class
* Default methods → used if class does NOT override
* Static methods → resolved at compile time via interface

---

# ❌ Common Mistakes

### 1. Trying to override static methods

Not allowed (they are not polymorphic)

---

### 2. Using default methods for heavy logic

Bad design → keeps business logic inside interface

---

### 3. Confusing default with abstract

Default = optional behavior
Abstract = mandatory behavior

---

# 🌍 Real-World Analogy

Think of a contract:

### Abstract method:

> “You MUST pay”

### Default method:

> “Here is how we usually validate payment”

### Static method:

> “Here is general information about payment systems”

---

# 🎯 Core Takeaway

> Interfaces are no longer just contracts — they can also provide shared behavior.

But:

✔ Use abstract for rules
✔ Use default for shared logic
✔ Use static for utilities

---

# 🚀 Next Step

Next we move into the most important concept in this module:

> **Chapter 04 — Polymorphism with Interfaces**

Where you will learn:

* how interface references unlock runtime flexibility
* how real systems switch behavior dynamically
* and why this is the core of professional Java design

Proceed when ready.
