
# Object-Oriented Programming (OOP) in Python — Complete Learning Repository

## 📌 Overview
This repository is a **complete beginner-to-intermediate guide** to **Object-Oriented Programming (OOP) in Python**.
It covers all **four pillars of OOP** with **clear explanations, real-world examples, use cases, and interview-oriented notes**.

This repository is designed for:
- Freshers / Entry-level developers
- Interview preparation (SDE-1, backend roles)
- Strong foundation before moving to **Low-Level Design (LLD)**

---

## 🧱 The Four Pillars of OOP

### 1️⃣ Classes & Objects
**What it is:**
- A class is a blueprint
- An object is an instance of a class

**Why it is used:**
- To model real-world entities
- To group data and behavior together

**Real-World Example:**
- Class: `Student`
- Object: `student1`, `student2`

**When to use:**
- When you need to represent real-world entities with attributes and actions

---

### 2️⃣ Inheritance
**What it is:**
- One class acquiring properties and methods of another class
- Represents an **IS-A relationship**

**Why it is used:**
- Code reusability
- Easy maintenance
- Logical hierarchy

**Real-World Example:**
- `Vehicle` → `Car`, `Bike`, `Truck`
- `Student` → `SchoolStudent`, `CollegeStudent`

**When to use:**
- When building a hierarchy
- When child classes share common behavior

**When NOT to use:**
- When relationship is HAS-A (use composition instead)

---

### 3️⃣ Polymorphism
**What it is:**
- Same method name behaving differently based on the object

**Why it is used:**
- Avoids large if-else chains
- Supports scalability
- Enables flexible designs

**Real-World Example:**
- `pay()` → UPI, Card, Wallet
- `send()` → Email, SMS, Push

**When to use:**
- Same action, different behavior
- System is expected to grow

**When NOT to use:**
- Simple logic
- Value-based operations (e.g., temperature conversion)

---

### 4️⃣ Abstraction
**What it is:**
- Hiding internal implementation details
- Showing only essential features

**Why it is used:**
- Reduce complexity
- Enforce structure
- Secure internal logic

**Real-World Example:**
- ATM system
- Payment gateway APIs
- Database drivers

**How it is achieved in Python:**
- Abstract Base Classes (`abc` module)

**When to use:**
- When you want to define a contract
- Large systems with multiple implementations

---

### 5️⃣ Encapsulation
**What it is:**
- Binding data and methods together
- Restricting direct access to data

**Why it is used:**
- Data protection
- Validation and security
- Prevent misuse

**Real-World Example:**
- Bank account balance
- User password
- Payment amount

**How it is achieved in Python:**
- Public (`variable`)
- Protected (`_variable`)
- Private (`__variable`)

**When to use:**
- Sensitive data
- Business rule enforcement

---

## 🔁 Relationship Between OOP Concepts
- **Inheritance** enables **Polymorphism**
- **Abstraction** defines WHAT to do
- **Polymorphism** defines HOW to do
- **Encapsulation** protects data
- All pillars work together in real systems

---

## 🏗 Real-World Systems Covered in This Repo
- Online Order System
- Payment Gateway
- Bank Account System
- Vehicle Management
- Student Enrollment System

Each example focuses on:
- Identifying entities
- Applying correct OOP principles
- Writing clean, interview-ready code

---

## 🎯 Interview Preparation Focus
This repository helps you answer:
- What are the four pillars of OOP?
- When to use inheritance vs composition?
- Difference between abstraction and encapsulation?
- How polymorphism works in Python?
- Real-world OOP design examples

---

## 🚀 Next Step After This Repo
After completing this repository, you are ready to move to:
- **Low-Level Design (LLD)**
- Design patterns
- System design interviews

---

## 📁 Repository Structure
```
├── inheritance/
├── polymorphism/
├── abstraction/
├── encapsulation/
├── examples/
└── README.md  (this file)
```

---

## 🟢 Final Note
This repository focuses on **clarity over complexity**.
Every concept is explained with **simple language**, **real-world use cases**, and **interview relevance**.

Happy Learning 🚀
