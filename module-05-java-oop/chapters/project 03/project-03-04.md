# 📦 Project 3 — Stage 4: Updating Product Information

Your Inventory Management System can now:

* ✅ Create products
* ✅ Store multiple products
* ✅ Search products
* ✅ List all products

However, inventory data changes over time.

Examples:

* A product's price changes.
* A product is renamed.
* A product receives a new product ID.

Instead of deleting the product and creating a new one, we should simply **update the existing object**.

---

# 🎯 Stage Goal

Implement the ability to update a product's information.

By the end of this stage, your application will be able to:

* Find a product by its ID
* Update its information
* Keep all validation rules
* Preserve encapsulation

---

# 📁 Project Structure

```text id="p3-stage4-structure"
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

# 🧠 Why Update the Existing Object?

Suppose we have:

```text id="current-product"
ID       : P001
Name     : Mechanical Keyboard
Price    : $89.90
Quantity : 10
```

The supplier increases the price to:

```text id="new-price"
$99.90
```

We don't need a new product.

It's still the same product.

Only one attribute changed.

Updating the existing object preserves its identity and stock information.

---

# 🏗️ Step 1 — Reuse `findProduct()`

One of the biggest advantages of OOP is code reuse.

Instead of searching again:

```java id="search-product"
Product product =
    findProduct(productId);
```

Use the existing method.

Never duplicate search logic.

---

# 🏗️ Step 2 — Create `updateProduct()`

Inside `InventoryManager`, create:

```java id="update-signature"
public boolean updateProduct(
    String currentId,
    String newId,
    String newName,
    double newPrice
)
```

Return:

* `true` → update successful.
* `false` → product not found.

---

# 🏗️ Step 3 — Find the Product

Inside the method:

```java id="find-call"
Product product =
    findProduct(currentId);
```

If:

```java id="null-check"
product == null
```

Return:

```java id="return-false"
false
```

Otherwise, continue.

---

# 🏗️ Step 4 — Update the Product

Use the setters.

```java id="update-fields"
product.setProductId(newId);

product.setName(newName);

product.setPrice(newPrice);
```

Notice that we do **not** modify the fields directly.

The setters already validate the data.

---

# 🧠 Why Use Setters?

Imagine someone tries:

```text id="invalid-price"
Price

-150
```

The setter prevents invalid data.

Without encapsulation:

```java id="bad-update"
product.price = -150;
```

The object would become invalid.

Using setters protects the object.

---

# 🏗️ Step 5 — Return Success

After updating:

```java id="success"
return true;
```

The caller decides what message to display.

---

# 🧪 Testing

Create:

```text id="original"
P001

Mechanical Keyboard

89.90
```

Call:

```java id="update-call"
manager.updateProduct(
    "P001",
    "P001",
    "RGB Mechanical Keyboard",
    99.90
);
```

Expected:

```text id="updated"
ID       : P001
Name     : RGB Mechanical Keyboard
Price    : $99.90
Quantity : 10
```

Notice that the quantity remains unchanged.

---

# 🧪 Testing Invalid Search

Attempt:

```java id="missing-update"
manager.updateProduct(
    "P999",
    "P999",
    "Unknown",
    50
);
```

Expected:

```text id="update-failed"
Product not found.
```

---

# 🧠 Internal Execution

Conceptually:

```text id="execution"
Main

↓

InventoryManager

↓

findProduct()

↓

Product found

↓

setProductId()

↓

setName()

↓

setPrice()

↓

Return true
```

Notice that the manager never modifies private fields directly.

---

# 💡 Code Reuse

Instead of writing:

```java id="duplicate-loop"
for (...)
```

inside `updateProduct()`, we simply reuse:

```java id="reuse-search"
findProduct()
```

This keeps the code shorter, cleaner, and easier to maintain.

---

# 🧠 Design Principle

### Product

Responsible for:

* Validating its own data
* Updating itself through setters

---

### InventoryManager

Responsible for:

* Finding products
* Coordinating updates

---

### Main

Responsible for:

* Calling the update
* Displaying results

Every class continues to perform exactly one job.

---

# 🏗️ Current Architecture

```text id="architecture"
                 Main
                   │
                   ▼
          InventoryManager
      ├── addProduct()
      ├── findProduct()
      ├── updateProduct()
      └── listProducts()
                   │
                   ▼
               Product
        ├── setProductId()
        ├── setName()
        └── setPrice()
```

This architecture allows us to change product information without breaking encapsulation.

---

# 🚀 Looking Ahead

Updating product information changes descriptive data.

But inventory systems also need to change **stock levels**.

Products are constantly:

* Receiving new shipments
* Being sold
* Being returned

Fortunately, the `Product` class already has:

* `increaseStock()`
* `decreaseStock()`

The next stage will connect those methods to the `InventoryManager`, just like you did with deposits and withdrawals in the Bank System.

---

# ✔️ Stage 4 Complete

Excellent!

Your Inventory Management System now supports:

* ✅ Creating products
* ✅ Storing products
* ✅ Searching products
* ✅ Updating product information
* ✅ Listing all products

You've also reinforced one of the most important OOP practices: **reuse existing methods instead of duplicating logic**, while keeping validation inside the object that owns the data.

## ▶️ Next Step

Continue to **Project 3 — Stage 5: Managing Product Stock**, where you'll connect the `InventoryManager` to each `Product`'s stock management methods, allowing inventory quantities to increase and decrease safely while enforcing all business rules.
