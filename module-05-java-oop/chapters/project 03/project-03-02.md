# 📦 Project 3 — Stage 2: Building the `Product` Class

The project structure is ready.

Now it's time to build the heart of the Inventory Management System.

Every product stored in the inventory will be represented by a `Product` object.

Just like:

* `Student` represented one student.
* `BankAccount` represented one bank account.

Now:

* `Product` represents one product.

This is one of the most important ideas in Object-Oriented Programming:

> **One object models one real-world entity.**

---

# 🎯 Stage Goal

By the end of this stage, the `Product` class will:

* Store product information
* Protect its data through encapsulation
* Validate its attributes
* Manage its own stock
* Calculate its own inventory value
* Display its own information

---

# 📁 Project Structure

```text id="p3-stage2-structure"
src/
├── Main.java
├── model/
│   └── Product.java
├── service/
│   └── InventoryManager.java
└── util/
```

Only `Product.java` will be implemented during this stage.

---

# 🏗️ Step 1 — Define the Attributes

Create the following private attributes:

```java id="p3-fields"
private String productId;
private String name;
private double price;
private int quantity;
```

Each attribute has a specific purpose.

### `productId`

A unique identifier for the product.

Example:

```text id="product-id-example"
P001
```

---

### `name`

Stores the product name.

Example:

```text id="product-name-example"
Mechanical Keyboard
```

---

### `price`

Stores the price of one unit.

Example:

```text id="price-example"
89.90
```

---

### `quantity`

Stores the number of units currently in stock.

Example:

```text id="quantity-example"
15
```

---

# 🧠 Why Are These Fields Private?

Suppose the attributes were public.

Someone could write:

```java id="bad-public"
product.price = -500;
product.quantity = -10;
```

Now the product contains invalid information.

Encapsulation prevents this.

Every modification must go through methods that validate the data.

---

# 🏗️ Step 2 — Create the Constructors

## Default Constructor

```java id="default-constructor"
public Product() {
    this("UNKNOWN", "Unnamed Product", 0.0, 0);
}
```

---

## Parameterized Constructor

```java id="parameterized-constructor"
public Product(
    String productId,
    String name,
    double price,
    int quantity
) {
    setProductId(productId);
    setName(name);
    setPrice(price);
    setQuantity(quantity);
}
```

Notice that the constructor uses the setters.

This ensures that validation also happens during object creation.

---

# 🏗️ Step 3 — Create Getters

Create getters for every attribute.

Example:

```java id="getter"
public double getPrice() {
    return price;
}
```

Getters allow other classes to read the object's data safely.

---

# 🏗️ Step 4 — Create Setters

Implement validation.

### Product ID

Rules:

* Cannot be `null`
* Cannot be blank

---

### Name

Rules:

* Cannot be `null`
* Cannot be blank

---

### Price

Rules:

* Cannot be negative

Example:

```text id="price-validation"
✔ 79.90

✔ 0.00

✘ -20.00
```

---

### Quantity

Rules:

* Cannot be negative

Example:

```text id="quantity-validation"
✔ 10

✔ 0

✘ -5
```

These rules keep every product in a valid state.

---

# 🏗️ Step 5 — Implement `increaseStock()`

Create:

```java id="increase-stock"
public boolean increaseStock(int amount)
```

Rules:

* Amount must be greater than zero.
* Increase the quantity.
* Return `true`.

Otherwise:

```java id="increase-fail"
return false;
```

Example:

```text id="increase-example"
Current Stock

20

+

15

=

35
```

---

# 🏗️ Step 6 — Implement `decreaseStock()`

Create:

```java id="decrease-stock"
public boolean decreaseStock(int amount)
```

Rules:

* Amount must be greater than zero.
* Enough units must exist in stock.

Example:

```text id="decrease-example"
Stock

20

Remove

5

=

15
```

If someone tries:

```text id="invalid-remove"
Stock

20

Remove

50
```

The operation fails.

The quantity remains unchanged.

---

# 🧠 Why Doesn't Another Class Modify the Quantity?

Imagine this:

```java id="bad-quantity"
product.quantity -= 50;
```

There is no validation.

The stock could become:

```text id="negative-stock"
-30
```

Instead:

```java id="good-quantity"
product.decreaseStock(50);
```

The object decides whether the operation is allowed.

---

# 🏗️ Step 7 — Calculate Total Value

Every product should know its own inventory value.

Create:

```java id="total-value"
public double calculateTotalValue()
```

Return:

```text id="formula"
price × quantity
```

Example:

```text id="calculation-example"
Price

80

×

Quantity

15

=

1200
```

This calculation belongs inside the `Product` class because it only depends on the product's own data.

---

# 🏗️ Step 8 — Display Product Information

Create:

```java
public void displayProductInformation()
```

Example output:

```text id="display-output"
----------------------------------
Product Information
----------------------------------
ID       : P001
Name     : Mechanical Keyboard
Price    : $89.90
Quantity : 15
Total    : $1348.50
----------------------------------
```

Notice that the method uses:

```java id="display-total"
calculateTotalValue();
```

Instead of calculating again.

This is another example of code reuse.

---

# 🧪 Testing

Update `Main.java`.

Create:

```java id="create-product"
Product keyboard =
    new Product(
        "P001",
        "Mechanical Keyboard",
        89.90,
        10
    );
```

Increase stock:

```java id="increase-test"
keyboard.increaseStock(5);
```

Decrease stock:

```java id="decrease-test"
keyboard.decreaseStock(2);
```

Display:

```java id="display-test"
keyboard.displayProductInformation();
```

Expected quantity:

```text id="quantity-result"
13
```

Calculation:

```text id="quantity-calculation"
10

+5

-2

=

13
```

Expected total value:

```text id="total-result"
89.90 × 13 = 1168.70
```

---

# ⚠️ Common Beginner Mistakes

## Allowing Negative Prices

Incorrect:

```java id="bad-price"
price = newPrice;
```

Always validate.

---

## Allowing Negative Stock

Incorrect:

```java id="bad-stock"
quantity -= amount;
```

Always verify available stock first.

---

## Duplicating Calculations

Bad:

```java id="duplicate"
price * quantity
```

inside multiple methods.

Instead:

```java id="reuse"
calculateTotalValue();
```

Write the calculation once and reuse it everywhere.

---

# 🧠 Design Principle

Each `Product` object is responsible for itself.

It knows:

* Its identity
* Its price
* Its stock
* Its total value

It does **not** know:

* Other products
* The inventory
* The total value of all products

Those responsibilities belong to another class.

---

# 🏗️ Current Architecture

```text id="current-architecture"
             Main
               │
               ▼
            Product

      ├── increaseStock()
      ├── decreaseStock()
      ├── calculateTotalValue()
      ├── displayProductInformation()
      ├── getters
      └── setters
```

The class is now complete and ready to become part of a larger inventory system.

---

# ✔️ Stage 2 Complete

Excellent!

You have built a fully encapsulated `Product` class that models a real inventory item instead of simply storing data.

It now:

* Protects its attributes
* Validates all modifications
* Manages its own stock
* Calculates its own inventory value
* Exposes behavior through well-defined methods

This is exactly how well-designed object-oriented classes behave.

## ▶️ Next Step

Continue to **Project 3 — Stage 3: Building the `InventoryManager` Class**, where you'll create the class responsible for managing multiple products, registering them, searching by product ID, and listing the inventory while keeping each `Product` focused solely on representing a single inventory item.
