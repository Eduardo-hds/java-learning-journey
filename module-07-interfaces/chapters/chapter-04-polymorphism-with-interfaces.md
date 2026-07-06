# Chapter 04 — Polymorphism with Interfaces

---

# 🧩 What We Are Learning Now

This is where interfaces become truly powerful.

We move from:

> “classes implementing interfaces”

to

> “systems that behave differently at runtime using the same code”

This concept is called:

> 🔁 Runtime Polymorphism (via interfaces)

---

# 🔷 1. What is Polymorphism (in this context)?

Polymorphism means:

> “One interface, many possible behaviors.”

With interfaces, it means:

* Same reference type
* Different actual objects
* Different runtime behavior

---

# 🧠 Core Idea

```java id="p1a2b3"
PaymentMethod payment;
```

This variable can hold:

* CreditCard
* PayPal
* PIX

So the *type is stable*, but the *behavior is flexible*.

---

# 🔷 2. Interface Reference in Action

```java id="c4d5e6"
PaymentMethod payment;

payment = new CreditCard();
payment.processPayment(100.0);

payment = new PayPal();
payment.processPayment(100.0);

payment = new PIX();
payment.processPayment(100.0);
```

---

## 🧠 What is happening?

Even though the variable type never changes:

* Java looks at the **actual object**
* Then decides which method to execute

---

# 🔥 3. Runtime Behavior Explained

When you call:

```java id="x7y8z9"
payment.processPayment(100.0);
```

Java does this:

1. Checks object in memory
2. Identifies actual class (CreditCard / PayPal / PIX)
3. Calls that implementation

This is called:

> 🧠 Dynamic Method Dispatch

---

# 💡 4. Why This Is Powerful

Without interfaces:

* You would need `if-else` everywhere
* Code becomes rigid
* Adding new types breaks existing logic

With interfaces:

✔ Add new class
✔ No need to change service code
✔ System automatically supports new behavior

---

# ❌ BAD Design (No Polymorphism)

```java id="bad123"
if (type == "creditcard") {
    processCreditCard();
} else if (type == "paypal") {
    processPayPal();
}
```

Problems:

* hard to maintain
* violates Open/Closed Principle
* every new method requires editing logic

---

# ✔ GOOD Design (Interface Polymorphism)

```java id="good123"
PaymentMethod payment = getPaymentMethod();
payment.processPayment(100);
```

No conditionals.
No coupling.
Fully extensible.

---

# 🌍 Real-World Example

Think of a checkout system:

* User selects payment method
* System does NOT care which one
* It just calls `processPayment()`

Behind the scenes:

* CreditCard system
* PIX system
* PayPal system

Same action → different behavior.

---

# 🧱 5. Polymorphism with Collections

Interfaces become even more powerful when used in lists:

```java id="list123"
List<PaymentMethod> methods = new ArrayList<>();

methods.add(new CreditCard());
methods.add(new PayPal());
methods.add(new PIX());

for (PaymentMethod method : methods) {
    method.processPayment(50.0);
}
```

---

## 🧠 What this shows

* One loop
* Multiple behaviors
* Fully dynamic execution

---

# ⚠️ Common Mistake

```java id="mistake123"
CreditCard payment = new CreditCard();
```

This removes polymorphism benefits because:

* You lock the system to one implementation
* You lose flexibility

---

# 🎯 Core Principle

> Always prefer interface types for variables, parameters, and collections.

This enables:

* flexibility
* scalability
* clean architecture

---

# 🌍 Real System Analogy

Think of a universal charger system:

Interface = “Charger”

Implementations:

* Apple charger
* USB-C charger
* Micro-USB charger

You plug in anything → system works the same way.

---

# 🧠 Key Insight

> Polymorphism is not about inheritance — it's about behavior substitution.

Interfaces are the cleanest way to achieve it.

---

# 🚀 Next Step

Now that you understand runtime flexibility, we will compare design approaches:

> **Chapter 05 — Interface vs Inheritance (Design Comparison)**

Where you will learn:

* when to use each one
* architectural differences
* and why professionals prefer interfaces for system design

Proceed when ready.
