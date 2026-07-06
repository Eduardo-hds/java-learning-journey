# 📦 Project 3 — Stage 3: Building the `InventoryManager` Class

Your `Product` class is now complete.

It can:

* ✅ Store product information
* ✅ Validate its data
* ✅ Increase stock
* ✅ Decrease stock
* ✅ Calculate its total value
* ✅ Display its own information

However, a store doesn't sell only one product.

An inventory may contain hundreds or even thousands of products.

To manage all of them, we need another class:

**`InventoryManager`**

Just like `StudentManager` and `BankManager`, this class will manage a collection of objects instead of representing a single object.

---

# 🎯 Stage Goal

By the end of this stage, your application will be able to:

* Store multiple products
* Register new products
* Search products by ID
* List every registered product

---

# 📁 Project Structure

```text id="p3-stage3-structure"
src/
├── Main.java
├── model/
│   └── Product.java
├── service/
│   └── InventoryManager.java
└── util/
```

Only `InventoryManager.java` will be implemented during this stage.

---

# 🧠 Why Do We Need an Inventory Manager?

Imagine asking a single product:

> "How many products are in the store?"

It can't answer.

A `Product` only knows about itself.

Instead:

```text
InventoryManager

↓

Knows every product
```

This follows the **Single Responsibility Principle**.

Each class has one clear purpose.

---

# 🏗️ Step 1 — Create the Attributes

Just like the previous projects, create:

```java
private Product[] products;
private int productCount;
```

### What do they represent?

`products`

Stores all registered products.

`productCount`

Keeps track of how many products are currently stored.

Initially:

```text
products

↓

[ null, null, null, ..., null ]
```

After registering two products:

```text
products

↓

[ Keyboard, Mouse, null, ..., null ]
```

```text
productCount

↓

2
```

---

# 🏗️ Step 2 — Create the Constructor

Initialize the inventory.

```java
public InventoryManager() {
    products = new Product[100];
    productCount = 0;
}
```

This project supports up to **100 products**.

---

# 🏗️ Step 3 — Register Products

Create:

```java
public boolean addProduct(Product product)
```

Responsibilities:

* Verify there is available space.
* Add the product.
* Increase `productCount`.
* Return `true`.

If the array is full:

```java
return false;
```

Notice that the manager **stores** products.

It does **not** create them.

---

# 🧠 Object Creation vs Object Storage

The flow is:

```text
Main

↓

Creates Product

↓

InventoryManager

↓

Stores Product
```

The manager owns the collection.

Each product owns its own data.

---

# 🏗️ Step 4 — Search Products

Create:

```java
public Product findProduct(String productId)
```

Loop only until:

```java
productCount
```

For each product:

```java
product.getProductId().equalsIgnoreCase(productId)
```

If found:

```java
return product;
```

Otherwise:

```java
return null;
```

---

# 🧠 Why Search by Product ID?

Imagine searching by name.

```text
USB Cable

USB Cable

USB Cable
```

Multiple products can have the same name.

The product ID should always be unique.

Example:

```text
P001

P002

P003
```

This makes searching reliable.

---

# 🏗️ Step 5 — List Products

Create:

```java
public void listProducts()
```

If there are no registered products:

```text
No products registered.
```

Otherwise:

Loop from:

```java
0
```

to:

```java
productCount - 1
```

For each product:

```java
product.displayProductInformation();
```

Notice that the manager doesn't know how to print a product.

It simply asks each product to display itself.

---

# 🧪 Testing

Update `Main.java`.

Create:

```java
Product keyboard =
    new Product(
        "P001",
        "Mechanical Keyboard",
        89.90,
        10
    );

Product mouse =
    new Product(
        "P002",
        "Gaming Mouse",
        39.90,
        20
    );

Product monitor =
    new Product(
        "P003",
        "27-inch Monitor",
        299.90,
        8
    );
```

Create the manager:

```java
InventoryManager manager =
    new InventoryManager();
```

Add the products:

```java
manager.addProduct(keyboard);
manager.addProduct(mouse);
manager.addProduct(monitor);
```

List everything:

```java
manager.listProducts();
```

Expected:

```text
----------------------------------
Product Information
----------------------------------
ID       : P001
Name     : Mechanical Keyboard
Price    : $89.90
Quantity : 10
Total    : $899.00
----------------------------------

----------------------------------
Product Information
----------------------------------
ID       : P002
Name     : Gaming Mouse
Price    : $39.90
Quantity : 20
Total    : $798.00
----------------------------------

----------------------------------
Product Information
----------------------------------
ID       : P003
Name     : 27-inch Monitor
Price    : $299.90
Quantity : 8
Total    : $2399.20
----------------------------------
```

---

# 🧪 Testing the Search

Search:

```java
Product product =
    manager.findProduct("P002");
```

If found:

```java
product.displayProductInformation();
```

Expected:

```text
Gaming Mouse
```

Search:

```text
P999
```

Expected:

```text
Product not found.
```

---

# 🧠 Internal Execution

Searching for:

```text
P002
```

Conceptually:

```text
P001

↓

Not a match

↓

P002

↓

Match found

↓

Return Product

↓

Search ends
```

As soon as the product is found, the search stops.

---

# 💡 Design Principle

Notice how the responsibilities remain perfectly separated.

### Product

Responsible for:

* Representing one product
* Managing its own stock
* Validating its own data
* Calculating its own value

---

### InventoryManager

Responsible for:

* Managing multiple products
* Registering products
* Searching products
* Listing products

---

### Main

Responsible for:

* Creating objects
* Calling methods
* Displaying results

Each class has one clear responsibility.

---

# 🏗️ Current Project Architecture

```text
                 Main
                   │
                   ▼
          InventoryManager
      ├── addProduct()
      ├── findProduct()
      └── listProducts()
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
      Product            Product
```

This architecture should now feel familiar.

You're applying the same object-oriented design pattern across different problem domains—a key skill for professional software development.

---

# 🚀 Looking Ahead

The inventory can now store and find products.

The next logical step is to allow products to change over time.

You'll implement:

* Updating product information
* Changing prices
* Renaming products

All while continuing to respect encapsulation and avoiding duplicated code.

---

# ✔️ Stage 3 Complete

Excellent!

Your Inventory Management System now supports:

* ✅ Creating products
* ✅ Storing multiple products
* ✅ Searching products by ID
* ✅ Listing all registered products

You now have the complete infrastructure needed to build a fully functional inventory system.

## ▶️ Next Step

Continue to **Project 3 — Stage 4: Updating Product Information**, where you'll reuse the search functionality to safely modify existing products through their public methods, reinforcing encapsulation and clean object collaboration.
