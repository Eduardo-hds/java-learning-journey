# 📦 Project 3 — Stage 7: Calculating the Total Inventory Value

Your Inventory Management System is almost complete.

Current features:

* ✅ Create products
* ✅ Store products
* ✅ Search products
* ✅ Update products
* ✅ Increase stock
* ✅ Decrease stock
* ✅ Remove products
* ✅ List all products

Now we'll add one final business feature that is extremely common in real inventory systems:

**Calculating the total value of the inventory.**

---

# 🎯 Stage Goal

Implement a method that calculates the combined value of every product currently stored in the inventory.

By the end of this stage, your application will be able to:

* Calculate the value of each product
* Sum the value of all products
* Display the total inventory value
* Reuse existing methods instead of duplicating calculations

---

# 📁 Project Structure

```text id="p3-stage7-structure"
src/
├── Main.java
├── model/
│   └── Product.java
├── service/
│   └── InventoryManager.java
└── util/
```

Only `InventoryManager` and `Main` will be updated.

---

# 🧠 Where Should This Calculation Be?

A common beginner question is:

> Should `Product` calculate the total inventory value?

No.

A `Product` only knows about itself.

For example:

```text id="single-product"
Mechanical Keyboard

Price: $89.90

Quantity: 10
```

It has no idea how many other products exist.

Instead:

```text id="manager-knows"
InventoryManager

↓

Knows every product
```

The manager is responsible for calculations involving **multiple products**.

---

# 🏗️ Step 1 — Reuse Existing Methods

Remember that every `Product` already has:

```java id="product-method"
calculateTotalValue()
```

Instead of calculating:

```java id="duplicate-formula"
price * quantity
```

again inside the manager, simply reuse the existing method.

This avoids duplicated code.

---

# 🏗️ Step 2 — Create the Method

Inside `InventoryManager`, create:

```java id="manager-method"
public double calculateInventoryValue()
```

Initially:

```java id="total-variable"
double total = 0;
```

Loop through every registered product.

For each product:

```java id="sum-values"
total += product.calculateTotalValue();
```

Finally:

```java id="return-total"
return total;
```

---

# 🧠 Internal Execution

Imagine the inventory contains:

```text id="products"
Keyboard

↓

$899
```

```text id="mouse"
Mouse

↓

$798
```

```text id="monitor"
Monitor

↓

$2399.20
```

Java conceptually performs:

```text id="execution"
total

↓

0

↓

+899

↓

1697

↓

+2399.20

↓

4096.20
```

Then returns:

```text id="result"
4096.20
```

---

# 🧪 Testing

Create:

```text id="inventory"
Keyboard

89.90

10
```

```text id="inventory2"
Mouse

39.90

20
```

```text id="inventory3"
Monitor

299.90

8
```

Call:

```java id="calculate"
double total =
    manager.calculateInventoryValue();
```

Display:

```java id="print"
System.out.printf(
    "Total Inventory Value: $%.2f%n",
    total
);
```

Expected:

```text id="expected"
Total Inventory Value: $4096.20
```

---

# 🧪 Testing Empty Inventory

Suppose there are no products.

Loop:

```text id="empty"
0 iterations
```

The variable remains:

```text id="zero"
total = 0
```

Return:

```text id="empty-result"
0.0
```

Output:

```text id="display-empty"
Total Inventory Value: $0.00
```

---

# 🧠 Why Doesn't `Product` Calculate Everything?

Imagine asking one product:

> "How much is the entire warehouse worth?"

It can't answer.

It only knows:

```text id="one-product"
Its own price

Its own quantity
```

The manager knows about **every** product.

Therefore, it performs calculations involving the entire collection.

---

# 💡 Code Reuse

Notice the chain of method calls:

```text id="chain"
InventoryManager

↓

calculateInventoryValue()

↓

Product

↓

calculateTotalValue()
```

Each class performs its own calculation.

No formulas are duplicated.

If tomorrow the calculation inside `Product` changes, the manager automatically benefits from the update.

---

# 🧠 Design Principle

### Product

Responsible for:

* Calculating its own value

---

### InventoryManager

Responsible for:

* Calculating the value of the entire inventory

---

### Main

Responsible for:

* Calling the method
* Displaying the result

This keeps responsibilities perfectly separated.

---

# 🏗️ Updated Architecture

```text id="architecture"
                 Main
                   │
                   ▼
          InventoryManager
      ├── addProduct()
      ├── findProduct()
      ├── updateProduct()
      ├── increaseStock()
      ├── decreaseStock()
      ├── removeProduct()
      ├── listProducts()
      └── calculateInventoryValue()
                   │
                   ▼
                Product
      ├── calculateTotalValue()
      ├── increaseStock()
      ├── decreaseStock()
      └── displayProductInformation()
```

Notice that every new feature has been added without breaking the existing architecture.

This is one of the biggest advantages of good object-oriented design.

---

# 🚀 Looking Ahead

Your Inventory Management System is now feature complete.

The only thing left is what every professional developer does before considering a project finished:

* Review the architecture
* Remove duplicated code
* Improve readability
* Verify responsibilities
* Test edge cases

This final refactoring stage will prepare your project as if it were ready to be delivered to a real client.

---

# ✔️ Stage 7 Complete

Excellent!

Your Inventory Management System now supports:

* ✅ Creating products
* ✅ Searching products
* ✅ Updating products
* ✅ Managing stock
* ✅ Removing products
* ✅ Listing products
* ✅ Calculating the total inventory value

You've also reinforced another key OOP principle: **complex operations should be built by combining simpler behaviors that already exist inside each object.**

## ▶️ Next Step

Continue to **Project 3 — Stage 8: Final Polish and Refactoring**, where you'll review the complete application, improve code quality, verify design decisions, and finish the final project of Module 05 with a clean, professional object-oriented architecture.
