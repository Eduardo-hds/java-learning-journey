# Chapter 02 — Defining and Implementing Interfaces

---

# 🧩 What You Will Learn Here

Now we move from concept → practice:

* How to define an interface
* How to implement it in classes
* How multiple classes can share the same contract
* How Java enforces the rules

This is where interfaces become *real code*, not just theory.

---

# 🧱 1. Defining an Interface

In Java, an interface is created using the `interface` keyword:

```java id="k2p8x1"
public interface PaymentMethod {
    void processPayment(double amount);
}
```

---

## 🧠 What this means

You are saying:

> “Any class that implements PaymentMethod MUST have a processPayment method.”

Important rules:

* No method body (for now)
* Only method signatures
* Acts like a contract

---

# 🧱 2. Implementing an Interface

A class uses an interface with the keyword `implements`:

```java id="m8q4ld"
public class CreditCard implements PaymentMethod {

    @Override
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment: " + amount);
    }
}
```

---

## 🧠 What is happening here?

* CreditCard is agreeing to follow the contract
* It MUST implement all interface methods
* If it doesn’t → compilation error

---

# 🧱 3. Multiple Implementations (Key Power of Interfaces)

You can create many classes using the same interface:

```java id="p3x9rt"
public class PayPal implements PaymentMethod {

    @Override
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment: " + amount);
    }
}
```

```java id="q7v2sa"
public class PIX implements PaymentMethod {

    @Override
    public void processPayment(double amount) {
        System.out.println("Processing PIX payment: " + amount);
    }
}
```

---

## 💡 Why this matters

Now you have:

* Same contract
* Different behaviors
* Interchangeable objects

This is the foundation of flexible systems.

---

# 🔁 4. Using Interface as a Type

This is the most important concept:

```java id="x1n5bz"
PaymentMethod payment = new CreditCard();
payment.processPayment(100.0);
```

---

## 🧠 What is happening?

Even though the object is `CreditCard`, the type is:

> PaymentMethod (interface reference)

This means:

* You are programming against the contract
* Not the concrete class

---

# ⚙️ 5. Runtime Behavior (VERY IMPORTANT)

```java id="r9k2mc"
PaymentMethod payment;

payment = new CreditCard();
payment.processPayment(100);

payment = new PIX();
payment.processPayment(100);
```

---

## 🔥 Result:

Same variable → different behavior

This is called:

> 🔁 Runtime Polymorphism

---

# 📌 When to Use Interface Type

Always prefer:

```java
PaymentMethod payment
```

Instead of:

```java
CreditCard payment
```

Why?

* More flexible
* Easier to extend
* Less code changes later

---

# ❌ Common Mistake

```java
CreditCard payment = new CreditCard();
```

This locks your system into one implementation.

Bad for scalable systems.

---

# 🌍 Real-World Analogy

Think of:

Interface = “Payment Terminal”

Implementations:

* Credit Card machine
* PIX scanner
* PayPal login

You don’t care how it works internally,
you just use the terminal.

---

# 🎯 Core Takeaway

> Interfaces allow you to treat different classes as the same type.

But behavior still changes internally.

---

# 🧪 Mini Exercise (Mental)

Imagine:

You create:

* `Transport` interface
* `Car`, `Bike`, `Bus`

Ask yourself:

1. What method would all of them share?
2. What would differ internally?
3. How would you switch between them without changing code?

---

# 🚀 Next Step

Next we go deeper into interface power:

> **Chapter 03 — Methods in Interfaces (abstract, default, static)**

Where you will learn:

* why interfaces are no longer “only abstract”
* how Java evolved them
* and how default methods change design flexibility

Proceed when ready.
