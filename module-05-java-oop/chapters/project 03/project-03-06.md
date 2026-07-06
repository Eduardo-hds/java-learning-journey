# 📦 Project 3 — Stage 6: Removing Products

Your Inventory Management System is becoming a complete application.

Current features:

* ✅ Create products
* ✅ Store products
* ✅ Search products
* ✅ Update product information
* ✅ Increase stock
* ✅ Decrease stock
* ✅ List all products

The next feature is the ability to **remove products** from the inventory.

This operation is very similar to removing students in Project 1.

The same array management technique applies here.

---

# 🎯 Stage Goal

Implement the ability to remove a product by its ID.

By the end of this stage, your application will be able to:

* Find a product
* Remove it from the array
* Shift the remaining products
* Keep the inventory organized
* Update the product count

---

# 📁 Project Structure

```text id="p3-stage6-structure"
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

# 🧠 Why Can't We Simply Set the Product to `null`?

Imagine the inventory contains:

```text id="inventory-before"
Index

0 → Keyboard
1 → Mouse
2 → Monitor
3 → Headset
```

If we remove the Mouse like this:

```java id="wrong-remove"
products[1] = null;
```

The array becomes:

```text id="inventory-gap"
Index

0 → Keyboard
1 → null
2 → Monitor
3 → Headset
```

Now there is an empty gap.

Every method that loops through the array would need to handle `null` values.

This makes the code more complicated and error-prone.

---

# 🧠 The Correct Solution

Instead of leaving a gap:

Move every product after the removed one one position to the left.

Example:

Before:

```text id="shift-before"
0 → Keyboard
1 → Mouse
2 → Monitor
3 → Headset
```

After removing Mouse:

```text id="shift-after"
0 → Keyboard
1 → Monitor
2 → Headset
3 → null
```

Finally:

```text id="decrease-count"
productCount--;
```

The inventory remains compact and organized.

---

# 🏗️ Step 1 — Create the Method

Inside `InventoryManager`, create:

```java id="remove-method"
public boolean removeProduct(String productId)
```

Return:

* `true` → product removed.
* `false` → product not found.

---

# 🏗️ Step 2 — Find the Product Index

Unlike `findProduct()`, we need the **position** of the product in the array.

Loop from:

```java id="loop-range"
0
```

to:

```java id="loop-end"
productCount - 1
```

Compare:

```java id="comparison"
products[i]
    .getProductId()
    .equalsIgnoreCase(productId)
```

When a match is found:

You have the index to remove.

---

# 🏗️ Step 3 — Shift the Products

Move every product after the removed one one position to the left.

Conceptually:

```text id="shift-process"
products[i]

↓

products[i + 1]

↓

products[i + 2]

↓

...

↓

Until the last product
```

This closes the empty space.

---

# 🏗️ Step 4 — Clear the Last Position

After shifting:

The final product exists twice.

Example:

```text id="duplicate-reference"
0 → Keyboard
1 → Monitor
2 → Headset
3 → Headset
```

Clear the duplicate reference:

```java id="clear-last"
products[productCount - 1] = null;
```

Now:

```text id="clean-array"
0 → Keyboard
1 → Monitor
2 → Headset
3 → null
```

This also allows Java's Garbage Collector to reclaim the removed object if there are no remaining references to it.

---

# 🏗️ Step 5 — Update the Counter

Decrease the number of registered products.

```java id="update-counter"
productCount--;
```

Now the inventory knows that one product has been removed.

---

# 🏗️ Step 6 — Return the Result

If the product was removed:

```java id="return-success"
return true;
```

If no matching product was found:

```java id="return-failure"
return false;
```

---

# 🧪 Testing

Suppose the inventory contains:

```text id="products-before"
Keyboard

Mouse

Monitor

Headset
```

Call:

```java id="remove-test"
manager.removeProduct("P002");
```

Expected:

```text id="removed-message"
Product removed successfully.
```

List the products:

```text id="products-after"
Keyboard

Monitor

Headset
```

No empty gaps remain.

---

# 🧪 Testing Invalid Removal

Attempt:

```java id="invalid-remove"
manager.removeProduct("P999");
```

Expected:

```text id="not-found"
Product not found.
```

The inventory remains unchanged.

---

# 🧠 Internal Execution

Conceptually:

```text id="execution-flow"
Find Product

↓

Shift Remaining Products

↓

Clear Last Position

↓

Decrease productCount

↓

Return true
```

Everything happens inside the manager because it owns the collection.

---

# ⚠️ Common Beginner Mistakes

## Leaving a Gap

Incorrect:

```java id="gap-code"
products[i] = null;
```

Result:

```text id="gap-result"
Keyboard

null

Monitor
```

---

## Forgetting `productCount--`

The manager still believes the removed product exists.

This causes incorrect loops and duplicate output.

---

## Forgetting to Clear the Last Position

After shifting:

```text id="duplicate-last"
Keyboard

Monitor

Headset

Headset
```

Always set the final used position to `null`.

---

# 💡 Design Principle

### Product

Responsible for:

* Representing one inventory item
* Managing its own state

---

### InventoryManager

Responsible for:

* Managing the collection
* Adding products
* Searching products
* Updating products
* Managing stock
* Removing products

---

### Main

Responsible for:

* Calling operations
* Displaying results

The separation of responsibilities remains clean.

---

# 🏗️ Current Project Architecture

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
      └── listProducts()
                   │
                   ▼
                Product
```

Your `InventoryManager` now supports the complete set of CRUD operations:

* **Create**
* **Read**
* **Update**
* **Delete**

This pattern is the foundation of countless inventory, e-commerce, ERP, and warehouse management systems.

---

# 🚀 Looking Ahead

Your inventory is now fully manageable.

But one important feature is still missing.

Managers often want to know:

> **"How much is my entire inventory worth?"**

Instead of calculating one product at a time, you'll create a method that calculates the **total value of all products combined**, reusing each product's own `calculateTotalValue()` method.

This is another excellent example of object collaboration and code reuse.

---

# ✔️ Stage 6 Complete

Excellent!

Your Inventory Management System now supports:

* ✅ Creating products
* ✅ Searching products
* ✅ Updating products
* ✅ Increasing stock
* ✅ Decreasing stock
* ✅ Removing products
* ✅ Listing all products

You've successfully reused the array management techniques from Project 1 while continuing to apply encapsulation and clean separation of responsibilities.

## ▶️ Next Step

Continue to **Project 3 — Stage 7: Calculating the Total Inventory Value**, where you'll combine the values of every product in the inventory, reuse existing object behavior, and complete the final major feature of your Inventory Management System.
