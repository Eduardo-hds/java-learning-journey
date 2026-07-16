# Chapter 31 — Exercise 2: Product Inventory System (Part 2)

In the previous chapter, we created:

* `Product` model.
* `InventoryService`.
* `HashMap<Integer, Product>`.
* Product registration.
* Product search by ID.

Now we will implement the remaining inventory operations:

* Update stock.
* Remove products.
* List products.
* Understand Map views.

---

# Current InventoryService

Currently:

```text id="s7m3q9"
InventoryService

+ addProduct()
+ findById()
```

We will add:

```text id="x8q4m2"
+ updateStock()
+ removeProduct()
+ listProducts()
```

---

# Part 1 — Updating Stock

Inventory systems constantly change.

Example:

Initial:

```text id="v5m8p1"
Keyboard
Quantity: 20
```

New shipment:

```text id="k9x3q7"
+50 units
```

Result:

```text id="n4m7q2"
Quantity: 70
```

---

# Wrong Approach

We could do:

```java id="d8p2x5"
product.quantity = 70;
```

But:

* Breaks encapsulation.
* Allows invalid values.

Example:

```java id="w6m3q9"
quantity = -100;
```

---

# Correct Approach

The Product controls stock changes.

We already created:

```java id="f7x2m8"
addStock()
```

---

# InventoryService Method

```java id="p4m9q6"
public void updateStock(
        int id,
        int amount){

    Product product =
            products.get(id);


    if(product != null){

        product.addStock(amount);

    }

}
```

---

# Flow

Example:

```java id="q8m5x3"
updateStock(
    1001,
    50
);
```

---

HashMap:

```text id="m2q7x9"
1001 → Keyboard
```

gets product.

---

Product:

```java id="r5m8p1"
addStock(50)
```

updates itself.

---

# Complexity

Search:

```text id="t7m3q8"
HashMap.get()
```

Average:

```text id="z4p9m2"
O(1)
```

---

# Part 2 — Removing Products

Requirement:

Remove product by ID.

Example:

Before:

```text id="h6m2q7"
1001 → Keyboard
1002 → Mouse
```

Remove:

```text id="n8x4p3"
1001
```

After:

```text id="c5m9q2"
1002 → Mouse
```

---

# Implementation

```java id="y3q7m5"
public void removeProduct(int id){

    products.remove(id);

}
```

---

# How remove() Works

HashMap:

```java id="v8m4q1"
remove(key)
```

uses:

```text id="x6m2p9"
hashCode()
equals()
```

to locate the entry.

---

# Complexity

Average:

```text id="w5q8m3"
O(1)
```

---

# Part 3 — Listing Products

A Map is not directly iterable like a List.

This does NOT work:

```java id="k9m3x7"
for(Product p : products)
```

Why?

Because a Map stores:

```text id="r2m8q4"
Key + Value
```

not only values.

---

# Map Views

Maps provide three important views:

---

# 1. keySet()

Returns all keys.

Example:

```java id="p7x3m9"
products.keySet();
```

Result:

```text id="m5q8v2"
1001
1002
1003
```

---

Example:

```java id="s8m2x6"
for(Integer id : products.keySet()){

    System.out.println(id);

}
```

Output:

```text id="d4m7q9"
1001
1002
1003
```

---

# 2. values()

Returns all values.

Example:

```java id="g6x2m8"
products.values();
```

Result:

```text id="q5m9p3"
Keyboard
Mouse
Monitor
```

---

For inventory, this is usually what we need.

---

Implementation:

```java id="h8m4q1"
public void listProducts(){

    for(Product product : products.values()){

        System.out.println(product);

    }

}
```

---

# 3. entrySet()

Returns both key and value.

Example:

```java id="z7m3x5"
products.entrySet();
```

Result:

```text id="n2q8p4"
1001 → Keyboard
1002 → Mouse
```

---

Example:

```java id="x4m9q6"
for(Map.Entry<Integer,Product> entry :
        products.entrySet()){


    System.out.println(
        entry.getKey()
    );


    System.out.println(
        entry.getValue()
    );

}
```

---

# Which One Should We Use?

## Need only products?

Use:

```java id="f6m2x8"
values()
```

Example:

"Print inventory."

---

## Need only IDs?

Use:

```java id="q9m4p1"
keySet()
```

Example:

"Generate product ID report."

---

## Need both?

Use:

```java id="v3m7q5"
entrySet()
```

Example:

"Export inventory."

---

# Part 4 — Checking Product Existence

Before removing:

```java id="j8m2q7"
if(products.containsKey(id)){

    products.remove(id);

}
```

---

Why?

Because:

```java id="x5m9p3"
remove()
```

does not complain if the key does not exist.

It simply returns:

```text id="m4q8x1"
null
```

---

# Part 5 — Inventory Service Complete

Now:

```text id="g7m3q9"
InventoryService

+ addProduct()
+ findById()
+ updateStock()
+ removeProduct()
+ listProducts()
```

---

# Testing Application

Main:

```java id="w2m8x5"
InventoryService service =
        new InventoryService();


Product keyboard =
        new Product(
            1001,
            "Keyboard",
            150,
            20
        );


service.addProduct(keyboard);


service.updateStock(
    1001,
    30
);


service.listProducts();
```

---

Expected:

```text id="p8m4q2"
Product{id=1001, name='Keyboard',
price=150.0, quantity=50}
```

---

# Comparing Student and Product Systems

## Student

Storage:

```java id="k4m7x9"
ArrayList<Student>
```

Reason:

* Ordered collection.
* Display all.
* Search not frequent.

---

## Product

Storage:

```java id="n8q3m5"
HashMap<Integer,Product>
```

Reason:

* ID lookup is primary.
* Fast access.
* Unique identifiers.

---

# Important Design Lesson

The collection should follow the domain.

Student:

> "Show me the students."

Product:

> "Find product with this ID."

Different problems.

Different collections.

---

# Common Mistakes

## Mistake 1 — Iterating Map incorrectly

Wrong:

```java
for(Product p : products)
```

Correct:

```java
for(Product p : products.values())
```

---

## Mistake 2 — Using List for everything

A List is not automatically the best option.

---

## Mistake 3 — Forgetting keys must be unique

This:

```java
put(1001, product)
```

replaces existing data.

---

# Exercise Task

Implement:

### InventoryService

* `updateStock()`
* `removeProduct()`
* `listProducts()`

Test:

1. Add products.
2. Increase stock.
3. Remove one.
4. Print inventory.

---

# ✔️ Next Step

In **Chapter 32 — Exercise 3: Unique Word Counter (Part 1)** we will combine:

* `Set`
* `HashSet`
* Duplicate prevention

and build a program that analyzes text by storing only unique words.
