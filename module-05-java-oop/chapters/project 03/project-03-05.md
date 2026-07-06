# 📦 Project 3 — Stage 5: Managing Product Stock

So far, your Inventory Management System can:

* ✅ Create products
* ✅ Store products
* ✅ Search products
* ✅ Update product information
* ✅ List all products

However, an inventory is constantly changing.

Products are:

* Delivered by suppliers
* Sold to customers
* Returned
* Restocked

This means the **quantity** of each product changes much more frequently than its name or price.

Fortunately, the `Product` class already knows how to manage its own stock.

Now, the `InventoryManager` will coordinate those operations.

---

# 🎯 Stage Goal

Implement stock management through the `InventoryManager`.

By the end of this stage, your application will be able to:

* Increase a product's stock
* Decrease a product's stock
* Prevent invalid stock operations
* Reuse the methods already implemented in `Product`

---

# 📁 Project Structure

```text id="p3-stage5-structure"
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

# 🧠 Why Doesn't the Manager Modify the Quantity?

Imagine writing:

```java id="bad-stock-update"
product.quantity += amount;
```

There are two problems:

* `quantity` is private.
* There is no validation.

Someone could accidentally write:

```java id="negative-stock"
product.quantity -= 500;
```

Result:

```text id="invalid-result"
Quantity

-470
```

Instead:

```java id="good-stock-update"
product.increaseStock(amount);

product.decreaseStock(amount);
```

The `Product` object decides whether the operation is valid.

---

# 🏗️ Step 1 — Create `increaseStock()`

Inside `InventoryManager`, create:

```java id="increase-manager"
public boolean increaseStock(
    String productId,
    int amount
)
```

Responsibilities:

1. Find the product.
2. If it doesn't exist:

```java id="increase-return"
return false;
```

3. Otherwise:

```java id="increase-call"
return product.increaseStock(amount);
```

Notice how little code is needed.

The manager delegates the work to the product.

---

# 🏗️ Step 2 — Create `decreaseStock()`

Create:

```java id="decrease-manager"
public boolean decreaseStock(
    String productId,
    int amount
)
```

Again:

Find the product.

If it doesn't exist:

```java id="decrease-false"
return false;
```

Otherwise:

```java id="decrease-call"
return product.decreaseStock(amount);
```

---

# 🧠 Code Reuse

Notice that the manager does **not** check:

```text id="validation"
Amount > 0

Enough stock
```

Why?

Because the `Product` already performs those validations.

Duplicating them would only make the code harder to maintain.

---

# 🧪 Testing Stock Increase

Suppose:

```text id="before-increase"
Keyboard

Quantity

10
```

Call:

```java id="increase-test"
manager.increaseStock(
    "P001",
    15
);
```

Expected:

```text id="after-increase"
Quantity

25
```

Calculation:

```text id="increase-calculation"
10

+15

=

25
```

---

# 🧪 Testing Stock Decrease

Current stock:

```text id="before-decrease"
25
```

Call:

```java id="decrease-test"
manager.decreaseStock(
    "P001",
    8
);
```

Expected:

```text id="after-decrease"
17
```

---

# 🧪 Testing Invalid Removal

Current stock:

```text id="current-stock"
17
```

Attempt:

```java id="too-many"
manager.decreaseStock(
    "P001",
    30
);
```

Expected:

```text id="failed"
Operation failed.
```

Quantity remains:

```text id="unchanged"
17
```

The product protects itself.

---

# 🧪 Testing Invalid Product

Attempt:

```java id="missing-product"
manager.increaseStock(
    "P999",
    10
);
```

Expected:

```text id="not-found"
Product not found.
```

---

# 🧠 Internal Execution

When executing:

```java id="stock-flow"
manager.increaseStock(
    "P001",
    20
);
```

Java performs something similar to:

```text id="flow"
Main

↓

InventoryManager

↓

findProduct()

↓

Product

↓

increaseStock()

↓

Return true
```

The manager never changes the quantity directly.

---

# 💡 Object Communication

This stage reinforces an important OOP principle.

The manager communicates with the product by sending messages:

```java id="messages"
increaseStock()

decreaseStock()
```

It never manipulates the object's private data.

Each object controls its own internal state.

---

# 🧠 Design Principle

### Product

Responsible for:

* Protecting stock
* Validating stock changes
* Updating quantity

---

### InventoryManager

Responsible for:

* Finding products
* Coordinating stock operations

---

### Main

Responsible for:

* Calling manager methods
* Displaying results

Every class continues to have exactly one responsibility.

---

# 🏗️ Updated Project Architecture

```text id="updated-architecture"
                 Main
                   │
                   ▼
          InventoryManager
      ├── addProduct()
      ├── findProduct()
      ├── updateProduct()
      ├── increaseStock()
      ├── decreaseStock()
      └── listProducts()
                   │
                   ▼
                Product
      ├── increaseStock()
      ├── decreaseStock()
      ├── calculateTotalValue()
      └── displayProductInformation()
```

Notice how similar this design is to the Bank System.

Instead of:

* Deposit
* Withdraw

We now have:

* Increase stock
* Decrease stock

Different business domain.

Exactly the same object-oriented principles.

---

# 🚀 Looking Ahead

The inventory can now create, update, search, and manage stock.

The next logical feature is removing products that are no longer sold.

You'll reuse the same array-shifting technique you learned in Project 1 to keep the inventory organized after removing a product.

---

# ✔️ Stage 5 Complete

Excellent!

Your Inventory Management System now supports:

* ✅ Creating products
* ✅ Searching products
* ✅ Updating product information
* ✅ Increasing stock
* ✅ Decreasing stock
* ✅ Listing all products

You've also reinforced one of the most important ideas in Object-Oriented Programming: **objects expose behavior through methods, while manager classes coordinate operations without violating encapsulation.**

## ▶️ Next Step

Continue to **Project 3 — Stage 6: Removing Products**, where you'll implement product deletion, reorganize the internal array after removals, and maintain a clean, gap-free inventory structure.
