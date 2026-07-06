# Chapter 6 — Real-World Modeling with Enums

Now we stop thinking about enums as isolated concepts and start using them the way they are used in real systems: **domain modeling**.

This is where enums become part of your application structure.

---

## 🧠 1. Order Status System (Core Model)

We already defined the enum:

```java id="m6o1"
public enum OrderStatus {
    PENDING,
    PROCESSING,
    SHIPPED,
    DELIVERED,
    CANCELLED
}
```

Now we use it in a real class.

---

### 📦 Order class (basic structure)

```java id="m6o2"
public class Order {

    private int id;
    private OrderStatus status;

    public Order(int id) {
        this.id = id;
        this.status = OrderStatus.PENDING;
    }

    public void setStatus(OrderStatus status) {
        this.status = status;
    }

    public void showStatus() {
        System.out.println("Order #" + id + " status: " + status);
    }
}
```

---

### 🧪 Usage in Main

```java id="m6o3"
public class Main {
    public static void main(String[] args) {

        Order order = new Order(1);

        order.showStatus();

        order.setStatus(OrderStatus.PROCESSING);
        order.showStatus();

        order.setStatus(OrderStatus.SHIPPED);
        order.showStatus();
    }
}
```

---

## 🧠 2. Why this is better than strings

### ❌ String version:

```java id="m6o4"
order.setStatus("SHIPPED");
```

Problems:

* typo risk
* no validation
* inconsistent states

---

### ✅ Enum version:

```java id="m6o5"
order.setStatus(OrderStatus.SHIPPED);
```

Benefits:

* compiler validation
* only valid states allowed
* easier refactoring

---

## 💳 3. Payment Type System

Now another real model.

### Enum:

```java id="m6p1"
public enum PaymentType {
    CREDIT_CARD,
    DEBIT_CARD,
    PIX,
    PAYPAL
}
```

---

### Usage in class:

```java id="m6p2"
public class Order {

    private PaymentType paymentType;

    public void setPaymentType(PaymentType paymentType) {
        this.paymentType = paymentType;
    }

    public void showPayment() {
        System.out.println("Payment: " + paymentType);
    }
}
```

---

## 🚦 4. User Role System (Access Control Model)

### Enum:

```java id="m6r1"
public enum UserRole {
    ADMIN,
    USER,
    GUEST
}
```

---

### Behavior example:

```java id="m6r2"
public class Main {
    public static void main(String[] args) {

        UserRole role = UserRole.ADMIN;

        switch (role) {
            case ADMIN:
                System.out.println("Full access granted.");
                break;

            case USER:
                System.out.println("Limited access.");
                break;

            case GUEST:
                System.out.println("Read-only access.");
                break;
        }
    }
}
```

---

## 🚦 5. Traffic Light Simulation (State Model)

We already saw logic, now think of it as a **state system**:

```java id="m6t1"
TrafficLight light = TrafficLight.RED;
```

Each enum value = a **system state**:

* RED → stop state
* YELLOW → transition state
* GREEN → active state

---

## 🧠 6. What you are really modeling

With enums you are not just writing code.

You are modeling:

| Concept          | Enum         |
| ---------------- | ------------ |
| Order lifecycle  | OrderStatus  |
| Payment methods  | PaymentType  |
| User permissions | UserRole     |
| System states    | TrafficLight |

---

## ⚖️ 7. Without enums vs With enums

### ❌ Without enums:

* string comparisons everywhere
* inconsistent values
* no structure

### ✅ With enums:

* centralized domain rules
* type-safe states
* readable business logic

---

## 🧠 8. Key Mental Shift

Instead of thinking:

> “What value should I store?”

Think:

> “What state or category does this belong to?”

That’s exactly what enums represent.

---

## 📌 Key Takeaway

Enums are not just constants.

They are:

> **domain modeling tools for representing fixed business rules**

---

# ✔️ Next Step

Now we move to advanced usage and real Java capabilities:

## Chapter 7 — Final Project: Order Management System

We will:

* combine all enums
* build state transitions
* use switch logic properly
* structure a full console system
