# Chapter 57 — Module 13 Final Assessment and Knowledge Consolidation

We have reached the end of **Module 13 — Collections Framework**.

The objective of this module was not to memorize classes like:

```java
ArrayList
HashMap
HashSet
TreeMap
```

The objective was to develop the ability to analyze a problem and choose the correct data structure.

The most important question from this module:

> What behavior does my application need from this collection?

---

# Final Project Evaluation

Our final project:

# Library Management System

was designed around real collection decisions.

---

# Book Storage

Requirement:

> Find books quickly by ID.

Chosen:

```java
Map<Integer, Book>
```

Implementation:

```java
HashMap<Integer, Book>
```

---

Why?

Because:

```java
books.get(id);
```

is the main operation.

Average complexity:

```text
O(1)
```

---

Wrong choices:

## List

Would require:

```java
for(Book book : books)
```

Complexity:

```text
O(n)
```

---

## Set

Would prevent duplicates, but searching by ID is not its purpose.

---

# User Storage

Requirement:

> Search users by identifier.

Chosen:

```java
Map<Integer, User>
```

---

Reason:

The key represents identity.

Example:

```text
User ID → User Object
```

---

# Borrow History

Requirement:

> Maintain the order of borrowing operations.

Chosen:

```java
List<BorrowRecord>
```

---

Why?

Because:

* Order matters.
* Duplicate records are valid.
* Sequential access is enough.

---

Example:

```text
1. Eduardo borrowed Clean Code

2. Maria borrowed Java

3. John borrowed Algorithms
```

---

A Set would be incorrect because:

```text
Same book can be borrowed multiple times.
```

---

# Waiting Queue

Requirement:

> First person waiting gets the book first.

Chosen:

```java
Queue<User>
```

---

Behavior:

FIFO:

```text
First In

First Out
```

---

Example:

Queue:

```text
Maria
John
Carlos
```

Processing:

```text
Maria
John
Carlos
```

---

A List could technically work, but Queue expresses the intention better.

---

# Categories

Requirement:

> Avoid duplicate categories.

Chosen:

```java
Set<String>
```

---

Example:

Input:

```text
Programming

Fantasy

Programming

```

Result:

```text
Programming

Fantasy
```

---

# Sorting System

Requirement:

> Generate different reports.

Solutions:

## Natural order

Used:

```java
Comparable
```

Example:

```text
Books sorted by title
```

---

## Custom orders

Used:

```java
Comparator
```

Examples:

```text
Books by author

Books by category

Books by price
```

---

# Complete Collection Framework Map

At the end of this module:

```text
Collections Framework


Iterable

    |

Collection

    |

+-----------+------------+

|           |            |

List        Set        Queue


Map

|

+-------------+-------------+

HashMap   LinkedHashMap   TreeMap
```

---

# Final Concept Review

---

# ArrayList

## Internal idea

Dynamic array.

---

Use when:

✅ Fast index access.

✅ Mostly reading.

---

Avoid when:

❌ Constant insertion/removal at beginning.

---

# LinkedList

## Internal idea

Nodes connected by references.

---

Use when:

✅ Many insertions/removals at ends.

---

Avoid when:

❌ Frequent random access.

---

# HashSet

## Internal idea

Hash table.

Uses:

```java
hashCode()

equals()
```

---

Use when:

✅ Need uniqueness.

---

Avoid when:

❌ Need ordering.

---

# LinkedHashSet

Adds:

```text
Insertion order
```

---

Use when:

✅ Need uniqueness + predictable iteration.

---

# TreeSet

Internal:

```text
Balanced tree
```

---

Use when:

✅ Need automatically sorted elements.

---

Cost:

```text
O(log n)
```

---

# HashMap

Most common Map.

---

Use when:

✅ Need fast key lookup.

Example:

```java
id → object
```

---

# LinkedHashMap

Adds:

```text
Insertion order
```

---

Use when:

✅ Need Map behavior + order.

---

# TreeMap

Adds:

```text
Sorted keys
```

---

Use when:

✅ Keys must stay ordered.

---

# Queue

Use when:

Need:

```text
FIFO
```

Examples:

* Waiting lines.
* Processing systems.
* Tasks.

---

# Deque

Use when:

Need both ends:

```text
First

Last
```

Can simulate:

* Queue.
* Stack.

---

# Iterator

Purpose:

Safely traverse collections.

---

Important:

Wrong:

```java
for(Book b : books){

    books.remove(b);

}
```

---

Correct:

```java
Iterator<Book> iterator =
        books.iterator();
```

---

# Most Common Mistakes

## Mistake 1

Using List for everything.

Example:

```java
List<User>
```

for searching by ID.

---

Better:

```java
Map<Integer,User>
```

---

## Mistake 2

Using HashSet expecting order.

Example:

```java
HashSet<String>
```

Output order is not guaranteed.

---

Need order?

Use:

```java
LinkedHashSet
```

---

## Mistake 3

Using TreeMap when ordering is unnecessary.

Example:

Need fast lookup only.

Use:

```java
HashMap
```

not:

```java
TreeMap
```

---

## Mistake 4

Forgetting equals() and hashCode()

Especially with:

* HashSet.
* HashMap keys.

---

## Mistake 5

Returning internal collections directly.

Example:

```java
return history;
```

Better:

```java
return Collections.unmodifiableList(history);
```

---

# Interview Questions

---

## Question 1

Why is HashMap fast?

Answer:

Because it uses hashing to locate values directly instead of searching sequentially.

---

## Question 2

Why can HashSet not contain duplicates?

Answer:

Because it uses hashCode and equals to determine whether an element already exists.

---

## Question 3

Difference between Comparable and Comparator?

Answer:

Comparable defines the natural ordering inside the class.

Comparator defines external custom sorting rules.

---

## Question 4

ArrayList or LinkedList?

Answer:

Usually ArrayList.

LinkedList only when frequent insertions/removals at the ends are required.

---

## Question 5

HashMap or TreeMap?

Answer:

HashMap:

```text
speed
```

TreeMap:

```text
sorted keys
```

---

# Final Skill Check

You should now be able to analyze:

---

## Scenario 1

"Store products and search by SKU."

Answer:

```java
HashMap<String, Product>
```

---

## Scenario 2

"Store unique usernames."

Answer:

```java
HashSet<String>
```

---

## Scenario 3

"Process customer requests in order."

Answer:

```java
Queue<Request>
```

---

## Scenario 4

"Display employees alphabetically."

Answer:

```java
List<Employee>

+

Comparator
```

---

## Scenario 5

"Keep a ranking always sorted."

Answer:

```java
TreeSet
```

or:

```java
TreeMap
```

depending on the requirement.

---

# Module 13 Completed

You have learned:

✅ Collections Framework purpose
✅ Collections hierarchy
✅ Iterable
✅ List
✅ ArrayList
✅ LinkedList
✅ Set
✅ HashSet
✅ LinkedHashSet
✅ TreeSet
✅ Queue
✅ Deque
✅ Map
✅ HashMap
✅ LinkedHashMap
✅ TreeMap
✅ Iterator
✅ ListIterator
✅ Comparable
✅ Comparator
✅ Collections utilities
✅ Performance analysis
✅ Collection selection strategies

---

# Final Takeaway

The professional Java developer does not ask:

> "Which collection syntax do I remember?"

The professional Java developer asks:

> "What behavior does my application need?"

Then chooses the structure that provides that behavior.

---

**End of Module 13 — Collections Framework** ✅

Next module can continue with the Bootcamp progression.
