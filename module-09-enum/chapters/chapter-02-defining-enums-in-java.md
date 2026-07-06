# Chapter 2 — Defining Enums in Java

Now we move from concept to **real code usage**.

---

## 🧠 1. Enum Keyword

In Java, enums are defined using the keyword:

```java id="e1k9ab"
enum
```

Basic structure:

```java id="v2m3qk"
public enum OrderStatus {
    PENDING,
    PROCESSING,
    SHIPPED,
    DELIVERED,
    CANCELLED
}
```

That’s it — this already creates a full type in Java.

---

## 🎯 2. What Happens When You Define an Enum?

When you write:

```java id="k3n8pp"
public enum PaymentType {
    CREDIT_CARD,
    DEBIT_CARD,
    PIX,
    PAYPAL
}
```

Java internally:

* Creates a special class
* Creates fixed instances for each constant
* Prevents new values from being created at runtime

So this is **NOT allowed**:

```java id="x8p2ld"
// ❌ Invalid
PaymentType p = new PaymentType();
```

---

## 🧪 3. Basic Usage

### Example in a variable:

```java id="q9m1aa"
PaymentType payment = PaymentType.PIX;

System.out.println(payment);
```

Output:

```
PIX
```

---

## 🧠 4. Enums in Switch (First Contact)

Enums are perfect for switch statements.

```java id="s7k2zz"
OrderStatus status = OrderStatus.PENDING;

switch (status) {
    case PENDING:
        System.out.println("Order is waiting.");
        break;
    case SHIPPED:
        System.out.println("Order is on the way.");
        break;
    default:
        System.out.println("Other status.");
}
```

👉 This is safer than using strings.

---

## ⚖️ 5. Enum vs String Constant (Real Difference)

### ❌ String approach:

```java id="l9q3tt"
String status = "shipped";

if (status.equals("SHIPPED")) {
    System.out.println("OK");
}
```

Problems:

* Case sensitivity issues
* Typo bugs
* No compiler validation

---

### ✅ Enum approach:

```java id="w2n8hh"
OrderStatus status = OrderStatus.SHIPPED;

if (status == OrderStatus.SHIPPED) {
    System.out.println("OK");
}
```

Benefits:

* No typos possible
* Faster comparison
* Cleaner code
* Compile-time safety

---

## 📌 6. Where Enums Go in Your Project

Following your structure:

```text id="proj09"
src/
 ├── model/
 │    ├── OrderStatus.java
 │    ├── PaymentType.java
 │    ├── TrafficLight.java
```

Each enum = one file.

Example:

```java id="file1"
package model;

public enum OrderStatus {
    PENDING,
    PROCESSING,
    SHIPPED,
    DELIVERED,
    CANCELLED
}
```

---

## 🧠 7. Key Rule

> Enum values are constants, but **typed constants**, not primitive strings or numbers.

---

## ❌ Common Mistakes

### 1. Treating enums like strings

```java id="err1"
if (status.equals("SHIPPED")) // ❌ wrong mindset
```

Correct:

```java id="err2"
if (status == OrderStatus.SHIPPED)
```

---

### 2. Trying to instantiate enums

```java id="err3"
// ❌ never possible
new OrderStatus();
```

---

## 🧪 8. Mini Practice (Important)

Try to understand this:

```java id="mini1"
OrderStatus status = OrderStatus.DELIVERED;

System.out.println(status.name());
System.out.println(status.ordinal());
```

We will fully explain `name()` and `ordinal()` later — just observe behavior for now.

---

## 🧠 Key Takeaway

* Enums define a **fixed set of values**
* They replace fragile string-based logic
* They improve readability and safety instantly
* Each enum constant is a real object

---

# ✔️ Next Step

Next we will go deeper into the **internal structure of enums in Java**:

## Chapter 3 — Enums in Java (Internal View)

We will learn:

* Why enums behave like classes
* How Java stores enum values internally
* What makes them different from normal classes