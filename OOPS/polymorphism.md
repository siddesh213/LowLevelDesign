# 📘 Polymorphism in Object-Oriented Programming (OOP) — Master Guide (Amazon & Microsoft Focused)

---

## ✅ Step 1: What is Polymorphism?

**Simple Definition:** Polymorphism means *many forms*. In object-oriented programming, it allows methods to perform different tasks based on the object that calls them.

**Real-World Analogy:** Think of the word "run" — a human can run, a machine can run, and a program can run. Same action name, different behaviors. That’s polymorphism.

**Long-Term Hint to Remember:**

> One interface, many implementations.

---

## ✅ Step 2: Where is Polymorphism Used in LLD (Low-Level Design)?

Polymorphism is fundamental in:

- **Designing flexible APIs**
- **Strategy Pattern** — for defining a family of interchangeable behaviors (Amazon interviews)
- **Factory Pattern** — for object creation based on input (Microsoft interviews)
- **Command Pattern** — for undoable operations (both Amazon & Microsoft)
- **SOLID Principles (OCP)** — Open/Closed Principle: Polymorphism helps extend functionality without changing existing code

---

## ✅ Step 3: Types & Subtypes of Polymorphism (with Examples)

### 🔹 1. Compile-Time Polymorphism (Method Overloading)

**Concept:**

- Same method name but different parameter list
- Resolved at compile time (Python simulates it via default args)

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c

c = Calculator()
print(c.add(2))       # 2
print(c.add(2, 3))    # 5
print(c.add(2, 3, 4)) # 9
```

> ⚠️ Python does not support true method overloading — the latest defined method overrides the previous one.

---

### 🔹 2. Runtime Polymorphism (Method Overriding)

**Concept:**

- Subclass provides a specific implementation of a method already defined in its superclass

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

class Cat(Animal):
    def speak(self):
        print("Cat meows")

for pet in [Dog(), Cat()]:
    pet.speak()  # Executes subclass method
```

✅ *Interview Use*: This is the most tested polymorphism in Amazon/Microsoft LLD rounds.

---

### 🔹 3. Interface-Based Polymorphism

**Concept:** Classes implement the same interface and can be used interchangeably.

```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class UPI(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} via UPI")

class CreditCard(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} via Credit Card")

for method in [UPI(), CreditCard()]:
    method.pay(500)
```

✅ *Interview Use*: Interface segregation and DIP (Dependency Inversion Principle)

---

### 🔹 4. Subtype Polymorphism

**Concept:** Subclass instance is treated as a parent type, but method behavior is resolved dynamically.

```python
class Vehicle:
    def drive(self):
        print("Generic drive")

class Car(Vehicle):
    def drive(self):
        print("Car driving")

def operate(vehicle: Vehicle):
    vehicle.drive()

operate(Car())  # Car driving
```

✅ *LLD Use*: Lets you pass around child objects without hard dependencies

---

### 🔹 5. Duck Typing (Python-Specific)

**Concept:** If an object behaves like a duck, we treat it like a duck. No inheritance required.

```python
class Dog:
    def speak(self):
        print("Bark")

class Cat:
    def speak(self):
        print("Meow")

def make_sound(animal):
    animal.speak()

make_sound(Dog())
make_sound(Cat())
```

✅ *Python Tip*: Focuses on behavior over structure.

---

## ✅ Step 4: Python Syntax Recap

```python
class Parent:
    def work(self):
        print("Parent works")

class Child(Parent):
    def work(self):
        print("Child studies")

obj = Child()
obj.work()  # Output: Child studies
```

---

## ✅ Step 5: Real-World Use Case

### 📦 Amazon Delivery System Example

Let’s say Amazon has a delivery system where:

- Each *Vehicle* has a method called `deliver()`.
- `Bike`, `Truck`, and `Drone` are different delivery methods, and each delivers differently.

```python
class Vehicle:
    def deliver(self):
        raise NotImplementedError

class Bike(Vehicle):
    def deliver(self):
        print("Delivering by Bike")

class Truck(Vehicle):
    def deliver(self):
        print("Delivering by Truck")

class Drone(Vehicle):
    def deliver(self):
        print("Delivering by Drone")

for v in [Bike(), Truck(), Drone()]:
    v.deliver()
```

✅ *LLD Angle*: Adds flexibility and removes conditional logic

---

## ✅ Step 6: Small Example — Interface-Based Polymorphism

```python
class Payment:
    def pay(self):
        raise NotImplementedError

class UPI(Payment):
    def pay(self):
        print("Paying via UPI")

class Card(Payment):
    def pay(self):
        print("Paying via Card")

for method in [UPI(), Card()]:
    method.pay()
```

---

## ✅ Step 7: Interview-Level Example (Amazon/Microsoft LLD)
# 📬 Notification System Design using Polymorphism (LLD Guide for Interviews)

This guide explains how to use **Polymorphism** to design a **Notification System** in Python that supports multiple channels (Email, SMS, Push). It’s built for **Low-Level Design (LLD)** interviews like those at **Amazon**, **Microsoft**, and similar top tech companies.

---

## 🔍 Problem Statement

**Design a Notification System that can send alerts via:**

- Email
- SMS
- Push Notification

---

## 🧠 Thought Process (How a Candidate Should Think in Interviews)

1. **Abstract the common behavior:**

   - All types of notifications have a `send()` action.
   - This means we can define a base class with a `send()` method.

2. **Use polymorphism to allow flexibility:**

   - Let each notifier class override `send()` with its specific logic.

3. **Make the system easily extensible:**

   - If tomorrow a new notifier (e.g., WhatsApp) is needed, just add a new subclass.

---

## 🔑 Key Concepts Used

### ✅ Interface-Based Polymorphism

Different classes implement the same method (`send()`), and the caller does not need to know the exact type.

### ✅ Run-Time Polymorphism

We decide at runtime which class’s `send()` method to execute.

---

## 📦 Class Structure

```
Notifier (Base Class)
│
├── EmailNotifier
├── SMSNotifier
└── PushNotifier
```

---

## 🧪 Python Implementation (Simple & Clean)

```python
from abc import ABC, abstractmethod

# Abstract Base Class
class Notifier(ABC):
    @abstractmethod
    def send(self, message: str):
        pass

# Subclass for Email
class EmailNotifier(Notifier):
    def send(self, message: str):
        print(f"Sending EMAIL: {message}")

# Subclass for SMS
class SMSNotifier(Notifier):
    def send(self, message: str):
        print(f"Sending SMS: {message}")

# Subclass for Push Notification
class PushNotifier(Notifier):
    def send(self, message: str):
        print(f"Sending PUSH Notification: {message}")

# ✅ Using Polymorphism
notifiers = [EmailNotifier(), SMSNotifier(), PushNotifier()]

for notifier in notifiers:
    notifier.send("Hello, this is your notification!")
```

---

## 🎯 Interview-Focused Explanation

- **Why Polymorphism?**

  - Clean, extensible design.
  - Open/Closed Principle: add new notifier without changing existing code.

- **What they test in interviews:**

  - Understanding of inheritance
  - Real-world modeling
  - Ability to design with future extensions in mind
  - Code clarity and use of abstract classes

---

## 🌍 Real-World Use Case

**E-commerce platform alerts**:

- Order confirmation via Email
- Delivery updates via SMS
- App offers via Push Notifications

All share the same `send()` behavior but use different channels.

---

## 🔄 Bonus: Extending with WhatsApp Notifier

```python
class WhatsAppNotifier(Notifier):
    def send(self, message: str):
        print(f"Sending WhatsApp Message: {message}")
```

Just add it to the list:

```python
notifiers.append(WhatsAppNotifier())
```

---

## 💡 Summary

| Feature            | Benefit                        |
| ------------------ | ------------------------------ |
| Interface/Abstract | Forces consistent structure    |
| Subclass `send()`  | Each has its own behavior      |
| Loosely coupled    | Easy to extend & test          |
| Polymorphic call   | Uniform method to trigger send |

This is a **classic polymorphism example** and **frequently asked** in LLD interviews.

---

## 🗣️ Use this when asked:

- "Design a notification system"
- "Show real-world use of polymorphism"
- "How would you make the system extensible?"

Always explain **why you chose polymorphism** and how it **helps scale and maintain** the system easily.

