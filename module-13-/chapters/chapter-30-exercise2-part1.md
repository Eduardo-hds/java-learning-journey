# Chapter 30 — Exercise 2: Product Inventory System (Part 1)

We finished the first exercise:

## Student Management System

We practiced:

* `ArrayList`
* Searching
* Removing
* Updating
* `equals()`
* Choosing between `List` and `Map`

Now we move to a scenario where a `Map` is a much more natural choice.

---

# Exercise Objective

Build a console-based inventory system.

The system will manage products using:

```java id="a2q8m5"
HashMap<Integer, Product>
```

The product ID will be the key.

---

# Why Use HashMap Here?

Think about a real inventory:

Example:

```text
Product ID

1001 → Keyboard
1002 → Mouse
1003 → Monitor
```

The main operation is:

> "Find product by its ID."

This is exactly what `HashMap` is designed for.

---

# Requirements

The system must support:

* Register products.
* Search products by ID.
* Update product stock.
* Remove products.
* List products.

---

# Project Structure

Continue using our module structure:

```text id="x6k3m9"
src/
│
├── Main.java
│
├── model/
│   ├── Student.java
│   └── Product.java
│
├── service/
│   ├── StudentService.java
│   └── InventoryService.java
│
└── util/
```

---

# Step 1 — Create Product Model

Location:

```text id="m4p7x2"
model/Product.java
```

The product represents our data.

---

Initial attributes:

```java id="b8q5n1"
public class Product {

    private int id;
    private String name;
    private double price;
    private int quantity;

}
```

---

# Why These Attributes?

## id

Identifier:

```text id="v3m8q4"
1001
```

Used as:

```java id="k9p2x6"
Map key
```

---

## name

Display information:

```text id="q7m3n5"
Keyboard
```

---

## price

Financial value:

```text id="h8x4p1"
99.90
```

---

## quantity

Inventory amount:

```text id="z5m2q8"
50 units
```

---

# Step 2 — Constructor

Create:

```java id="f4x8m2"
public Product(
        int id,
        String name,
        double price,
        int quantity){

    this.id = id;
    this.name = name;
    this.price = price;
    this.quantity = quantity;

}
```

---

# Step 3 — Getters

We need access:

```java id="y3q7m9"
public int getId(){
    return id;
}
```

---

```java id="p8m4x1"
public String getName(){
    return name;
}
```

---

```java id="n5q9v2"
public double getPrice(){
    return price;
}
```

---

```java id="r6m2x8"
public int getQuantity(){
    return quantity;
}
```

---

# Step 4 — Stock Update Methods

A product quantity should not be modified directly.

Avoid:

```java id="m9x3q7"
product.quantity = -500;
```

---

Create behavior:

```java id="t5p8n2"
public void addStock(int amount){

    quantity += amount;

}
```

---

Remove stock:

```java id="w7m4q9"
public void removeStock(int amount){

    if(amount <= quantity){

        quantity -= amount;

    }

}
```

---

# Why Put This Logic Inside Product?

Because the object understands its own rules.

Bad:

```text id="j8q5m3"
InventoryService changes Product internals
```

Better:

```text id="x4m9p7"
Product controls valid changes
```

This follows object-oriented design.

---

# Step 5 — Override toString()

Add:

```java id="k2q8m5"
@Override
public String toString(){

    return "Product{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", price=" + price +
            ", quantity=" + quantity +
            '}';

}
```

---

Now:

```java id="m6x3p9"
System.out.println(product);
```

shows:

```text
Product{id=1001, name='Keyboard', price=150.0, quantity=20}
```

---

# Step 6 — Create InventoryService

Location:

```text id="v9m2q5"
service/InventoryService.java
```

---

The collection:

```java id="s3x8m1"
private Map<Integer, Product> products =
        new HashMap<>();
```

---

# Why Map Instead of List?

Compare:

## List

```java id="g7m4x2"
products.get(1001);
```

Impossible.

A List uses:

```text id="p5q8n3"
index
```

not ID.

---

## Map

```java id="z2m9x6"
products.get(1001);
```

Direct lookup.

---

# Step 7 — Add Product

Method:

```java id="h8q3m7"
public void addProduct(Product product){

    products.put(
        product.getId(),
        product
    );

}
```

---

Example:

```java id="f6m1p9"
Product keyboard =
    new Product(
        1001,
        "Keyboard",
        150,
        20
    );


service.addProduct(keyboard);
```

---

Internal Map:

```text id="c7x2m5"
1001 → Keyboard
```

---

# Important HashMap Behavior

If we add:

```java id="q8m4v1"
products.put(
    1001,
    new Product(...)
);
```

again:

The old product is replaced.

Example:

Before:

```text id="s6p9m3"
1001 → Keyboard
```

After:

```text id="v4q7x2"
1001 → Mouse
```

---

# Preventing Duplicate IDs

Business rule:

> Product IDs must be unique.

Before adding:

```java id="r3m8q5"
if(products.containsKey(product.getId())){

    System.out.println(
        "Product already exists"
    );

}
```

---

# containsKey()

Very important Map method:

```java id="y5p2x9"
products.containsKey(id);
```

Checks if a key exists.

Complexity:

Average:

```text id="k7m4q3"
O(1)
```

---

# Step 8 — Find Product

Method:

```java id="w8m5x1"
public Product findById(int id){

    return products.get(id);

}
```

---

Example:

```java id="n4q9m6"
Product product =
        service.findById(1001);
```

---

Complexity:

Average:

```text id="z6p3m8"
O(1)
```

---

# Current InventoryService

Implemented:

```text id="h2x7m9"
InventoryService

+ addProduct()
+ findById()
```

---

# Comparing With Student System

Student:

```java id="m7q4x8"
ArrayList<Student>
```

Search:

```text id="r9p2m5"
O(n)
```

---

Product:

```java id="x3m8q1"
HashMap<Integer,Product>
```

Search:

```text id="v5q7m2"
O(1)
```

---

# Exercise Task

Create:

### Product.java

Implement:

* Fields.
* Constructor.
* Getters.
* Stock methods.
* toString().

---

### InventoryService.java

Implement:

* HashMap storage.
* addProduct().
* findById().

---

Test:

Create:

```text id="b4m8q6"
Keyboard
ID:1001

Mouse
ID:1002
```

Search:

```text id="n7x3p5"
1002
```

Expected:

```text id="k5m9q2"
Mouse
```

---

# ✔️ Next Step

In **Chapter 31 — Exercise 2: Product Inventory System (Part 2)** we will implement:

* Update stock.
* Remove products.
* List all products using `values()`.
* Understand `keySet()`, `values()`, and `entrySet()`.
* Analyze why Maps are ideal for inventory systems.
