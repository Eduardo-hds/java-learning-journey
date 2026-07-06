# Chapter 06 — Real-World Design with Interfaces

---

# 🧩 What This Chapter Is About

Now we stop thinking in isolated concepts and start thinking like a system designer.

You will learn how interfaces are used to:

* decouple layers
* switch behavior at runtime
* build scalable structures
* avoid hard dependencies

This is exactly how real Java systems are designed.

---

# 🔷 1. The Problem Without Interfaces

Imagine this service:

```java id="bad1"
class PaymentService {
    void payWithCreditCard(double amount) {
        System.out.println("Credit card payment: " + amount);
    }
}
```

---

## ❌ Problem

Now if you want:

* PayPal
* PIX
* Apple Pay

You must modify this class every time.

This leads to:

* rigid code
* constant modifications
* high risk of bugs

---

# 🔷 2. Introducing Interfaces (Fixing the Problem)

We define a contract:

```java id="good1"
interface PaymentMethod {
    void processPayment(double amount);
}
```

---

## Now implementations:

```java id="impl1"
class CreditCard implements PaymentMethod {
    public void processPayment(double amount) {
        System.out.println("Credit Card: " + amount);
    }
}
```

```java id="impl2"
class PIX implements PaymentMethod {
    public void processPayment(double amount) {
        System.out.println("PIX: " + amount);
    }
}
```

---

# 🔷 3. Service Layer Decoupling

Now the important part:

```java id="service1"
class PaymentService {

    void process(PaymentMethod method, double amount) {
        method.processPayment(amount);
    }
}
```

---

## 🧠 What changed?

Before:

* service knew everything

Now:

* service knows NOTHING about implementations

It only knows:

> “I accept anything that is a PaymentMethod.”

---

# 🔥 4. Runtime Flexibility

```java id="runtime1"
PaymentService service = new PaymentService();

PaymentMethod credit = new CreditCard();
PaymentMethod pix = new PIX();

service.process(credit, 100);
service.process(pix, 100);
```

---

## 🧠 Result

Same service → different behaviors

No changes needed in service code.

---

# 🌍 5. Real-World Architecture Thinking

This pattern is everywhere:

### Layers:

* Controller (input)
* Service (logic)
* Interface (contract)
* Implementation (behavior)

---

## Example mental model:

```
User Input
   ↓
Service (doesn't care how)
   ↓
Interface
   ↓
Concrete Implementation
```

---

# 🔷 6. Why This Design Is Powerful

## ✔ 1. Easy to extend

Add new payment type:

```java id="new1"
class CryptoPayment implements PaymentMethod {
    public void processPayment(double amount) {
        System.out.println("Crypto payment: " + amount);
    }
}
```

No changes anywhere else.

---

## ✔ 2. Easy to test

You can create fake implementations:

```java id="test1"
class FakePayment implements PaymentMethod {
    public void processPayment(double amount) {
        System.out.println("TEST PAYMENT");
    }
}
```

---

## ✔ 3. Loose coupling

Service is independent of implementation.

This is called:

> 🔗 Dependency Inversion Principle (basic idea)

---

# ❌ 7. What NOT to Do

### Bad design:

```java id="bad2"
PaymentService service = new PaymentService();
service.processCreditCard();
service.processPIX();
```

Problems:

* service becomes overloaded
* logic spreads everywhere
* no flexibility

---

# 🧠 8. Key Mental Shift

Before:

> “My service should know how everything works”

After:

> “My service should only know contracts”

---

# 🌍 9. Real Systems That Use This

Interfaces are used in:

* payment gateways
* notification systems
* logging frameworks
* file storage systems
* database drivers

---

## Example idea:

* MySQL driver vs PostgreSQL driver
* Same interface
* Different implementations

---

# 🎯 Core Concept of This Chapter

> Interfaces allow systems to grow without modification.

This is the foundation of scalable software.

---

# 🚀 Next Step

Now we will practice everything you learned:

> **Chapter 07 — Practice Systems (Guided Exercises)**

Where we will build:

* Payment system
* Notification system
* Animal system
* Transport system

Step by step, using interfaces correctly.

Proceed when ready.
