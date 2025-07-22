# 📘 LLD – Day 2: Classes & Objects (Amazon-level Explanation for Freshers)

📌 This is the most important building block in object-oriented design. If you master this deeply, every system you design (BookMyShow, Zomato, Cart, Splitwise) becomes 10x cleaner.

---

## 🧠 1. Real-World Understanding (Simple Analogy)

- Think of a **class** as a **blueprint** — like an architect’s drawing of a house.
- An **object** is a **real house** built using that blueprint.

---

## 📘 2. What is a Class?

A class is a blueprint that defines:

- The data each object will have (called **attributes** or **variables**)
- The actions it can perform (called **methods** or **functions**)

---

## 🔧 3. Python Syntax: Defining a Class

```python
class Car:
    def __init__(self, color, make, model, year):
        self.color = color     # state
        self.make = make       # state
        self.model = model     # state
        self.year = year       # state

    def display_info(self):    # behavior
        print(f"Car Make: {self.make}")
        print(f"Car Model: {self.model}")
        print(f"Car Year: {self.year}")
        print(f"Car Color: {self.color}")
```

---

## 🔍 Let’s Break This Down Like a Beginner:

| Part              | Meaning                                     |
| ----------------- | ------------------------------------------- |
| `class Car:`      | Declares a new class named `Car`            |
| `__init__`        | Constructor — called when object is created |
| `self.color` etc. | Instance variables                          |
| `display_info()`  | Method (action) for the object              |

---

## 🚗 4. What is an Object?

- An object is a **real thing** created from a class.
- Each object has its own data (**state**) and can perform actions (**behavior**).

### 🔧 Python Syntax: Creating Objects

```python
car1 = Car("Red", "Toyota", "Corolla", 2020)
car2 = Car("Blue", "Ford", "Mustang", 2021)

car1.display_info()
print("-----------")
car2.display_info()
```

### 💡 Output:

```
Car Make: Toyota
Car Model: Corolla
Car Year: 2020
Car Color: Red
-----------
Car Make: Ford
Car Model: Mustang
Car Year: 2021
Car Color: Blue
```

---

## 🗣️ 5. Interview-Style Speak

**"What is a class and object?"**

Say this:

> “A class is a blueprint for creating objects. It defines the structure (state) and behavior (methods) of objects. An object is an instance of a class with its own data. For example, a Car class defines what a car is, and each car1, car2 is an object with real data.”

---

## ✅ 6. Real-World Use in Amazon Systems

### Example: In a Cart System

```python
class CartItem:
    def __init__(self, product, quantity):
        self.product = product
        self.quantity = quantity

    def get_total_price(self):
        return self.product.price * self.quantity
```

You’ll later design:

- User
- Product
- Cart
- CartItem
- CheckoutService

All are **classes**, and you’ll create **objects** in real systems.

---

## 🔁 7. BONUS: How Amazon May Ask

**Interviewer:**

“Can you define a class for a Library system?”

You might answer:

```python
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn

    def display(self):
        print(f"{self.title} by {self.author}")

book1 = Book("Harry Potter", "J.K. Rowling", "123456")
book1.display()
```

---

## 📌 8. Summary Table (Takeaway Sheet)

| Term        | Meaning                                     |
| ----------- | ------------------------------------------- |
| Class       | Blueprint defining object structure         |
| Object      | Instance of a class with real data          |
| Attribute   | Variables/data inside the object            |
| Method      | Function that performs action               |
| Constructor | `__init__()` used to initialize object data |