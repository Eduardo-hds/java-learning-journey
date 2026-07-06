# Chapter 5 — Enums with Logic

Now we reach one of the most important uses of enums:

> Using enums to control behavior (not just store values)

This is where enums stop being “lists of constants” and start becoming **state controllers**.

---

## 🧠 1. Why add logic to enums?

Normally people use enums like this:

```java
OrderStatus status = OrderStatus.SHIPPED;
```

But real systems need behavior:

* What should happen in each state?
* What action is allowed?
* What message should be shown?

Enums help you centralize this logic.

---

## 🔁 2. Switch with Enums

This is the most common pattern.

### Example: OrderStatus behavior

```java id="c5s1"
public class Main {
    public static void main(String[] args) {

        OrderStatus status = OrderStatus.SHIPPED;

        switch (status) {
            case PENDING:
                System.out.println("Order is waiting for processing.");
                break;

            case PROCESSING:
                System.out.println("Order is being prepared.");
                break;

            case SHIPPED:
                System.out.println("Order is on the way.");
                break;

            case DELIVERED:
                System.out.println("Order completed.");
                break;

            case CANCELLED:
                System.out.println("Order was cancelled.");
                break;
        }
    }
}
```

---

## 🧠 3. Why this is powerful

Instead of scattered `if` statements:

```java
if (status == PENDING) { }
if (status == SHIPPED) { }
```

You now have:

* centralized logic
* clear structure
* safer control flow

---

## 🚦 4. Traffic Light Simulation (Core Exercise)

Now let's model real behavior.

### Enum:

```java id="c5s2"
public enum TrafficLight {
    RED,
    YELLOW,
    GREEN
}
```

---

### Behavior using switch:

```java id="c5s3"
public class Main {
    public static void main(String[] args) {

        TrafficLight light = TrafficLight.RED;

        switch (light) {
            case RED:
                System.out.println("STOP");
                break;

            case YELLOW:
                System.out.println("SLOW DOWN");
                break;

            case GREEN:
                System.out.println("GO");
                break;
        }
    }
}
```

---

## 🧠 5. What enums improve here

Without enums:

* You might use strings like `"red"`
* Or numbers like `1, 2, 3`
* Both are fragile

With enums:

* Only valid states exist
* Compiler protects logic
* Code becomes self-explanatory

---

## ⚖️ 6. Enum Logic vs If-Else Chains

### ❌ Bad approach:

```java
if (status == OrderStatus.PENDING) { }
else if (status == OrderStatus.SHIPPED) { }
else if (status == OrderStatus.DELIVERED) { }
```

### Why it's bad:

* hard to maintain
* grows messy fast
* easy to forget cases

---

### ✅ Better approach (switch):

```java
switch (status) {
    case PENDING:
    case SHIPPED:
}
```

---

## 🧠 7. Real-world mental model

Think of enums as:

> “State machines without complexity”

Each enum value represents a **state**, and switch defines **behavior per state**.

---

## 📌 8. Best Practice

✔ Use switch for:

* simple behavior mapping
* display messages
* state handling

❌ Avoid:

* deeply nested logic inside switch
* repeating switch in many classes (we will improve this later conceptually)

---

## 🧪 9. Mini Exercise

Try to predict output:

```java
TrafficLight light = TrafficLight.GREEN;

switch (light) {
    case RED:
        System.out.println("Stop");
        break;
    case GREEN:
        System.out.println("Go");
        break;
}
```

👉 Output?
Only:

```
Go
```

---

## 🧠 Key Takeaway

Enums are not just values.

They are:

> **state identifiers used to control behavior safely and clearly**

---

# ✔️ Next Step

Now we will apply enums to real modeling:

## Chapter 6 — Real-World Modeling with Enums

We will build:

* Order system status flow
* Payment types
* User roles
* And start combining enums with classes
