# Chapter 4 — Enum Utility Methods

Now we move into the **practical toolbox** of enums in Java.

These built-in methods are what make enums extremely powerful in real applications.

---

## 🧠 1. `values()` — Get All Enum Constants

### What it is

`values()` returns an **array of all enum constants** in the order they are declared.

---

### Example:

```java id="u4v1"
for (OrderStatus status : OrderStatus.values()) {
    System.out.println(status);
}
```

### Output:

```text id="u4v2"
PENDING
PROCESSING
SHIPPED
DELIVERED
CANCELLED
```

---

### Why it exists

It allows you to:

* iterate all possible values
* build menus
* validate inputs
* display options dynamically

---

### Real-world use:

```java id="u4v3"
System.out.println("Select status:");
for (OrderStatus status : OrderStatus.values()) {
    System.out.println("- " + status);
}
```

---

## 🧠 2. `valueOf()` — Convert String → Enum

### What it is

`valueOf()` converts a **String into an enum constant**.

---

### Example:

```java id="u4v4"
OrderStatus status = OrderStatus.valueOf("SHIPPED");

System.out.println(status);
```

### Output:

```text id="u4v5"
SHIPPED
```

---

### ⚠️ Important Risk

If the string does NOT match exactly:

```java id="u4v6"
OrderStatus.valueOf("shipped"); // ❌ ERROR
```

It throws:

```
IllegalArgumentException
```

---

### Why this matters

* Enforces strict matching
* Case-sensitive
* Prevents silent bugs

---

### Safe usage pattern:

```java id="u4v7"
try {
    OrderStatus status = OrderStatus.valueOf(input);
    System.out.println("Valid status: " + status);
} catch (IllegalArgumentException e) {
    System.out.println("Invalid status!");
}
```

---

## 🧠 3. `ordinal()` — Position Index (DANGEROUS)

### What it is

Returns the **index position** of the enum constant.

```java id="u4v8"
System.out.println(OrderStatus.PENDING.ordinal());
```

Output:

```text id="u4v9"
0
```

---

### Full list example:

```java id="u4v10"
for (OrderStatus status : OrderStatus.values()) {
    System.out.println(status + " -> " + status.ordinal());
}
```

---

### ⚠️ Why ordinal() is risky

If you change order:

```java id="u4v11"
PENDING,
SHIPPED,
PROCESSING
```

Everything breaks logically.

👉 So:

* NEVER use `ordinal()` for business logic
* ONLY use for debugging or display experiments

---

## ⚖️ 4. Enum Utility Methods Summary

| Method      | Purpose               | Safe for logic? |
| ----------- | --------------------- | --------------- |
| `values()`  | Get all constants     | ✅ Yes           |
| `valueOf()` | Convert string → enum | ⚠️ Carefully    |
| `ordinal()` | Position index        | ❌ No            |

---

## 🧪 5. Practical Console Example

### Simulating user input:

```java id="u4v12"
String input = "DELIVERED";

OrderStatus status = OrderStatus.valueOf(input);

switch (status) {
    case PENDING:
        System.out.println("Order is waiting.");
        break;
    case DELIVERED:
        System.out.println("Order completed.");
        break;
    default:
        System.out.println("Other state.");
}
```

---

## 🧠 6. Why These Methods Matter

These methods allow enums to behave like:

* a controlled dataset
* a safe input system
* a type-safe configuration system

Instead of writing:

```text id="u4v13"
if (status == "SHIPPED")
```

You build:

```text id="u4v14"
OrderStatus.SHIPPED
```

---

## 📌 Key Takeaway

Enums become powerful when you combine:

* `values()` → iterate options
* `valueOf()` → parse input
* `switch` → control behavior

---

# ✔️ Next Step

Next we will start **real behavior design with enums**:

## Chapter 5 — Enums with Logic

We will learn:

* switch with enums in real systems
* behavior per enum state
* building clean state-driven logic (Traffic Light system)