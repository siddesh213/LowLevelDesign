# Abstraction in Python — Complete Guide

## ⭐ 1. What is Abstraction?
Abstraction means **hiding unnecessary internal details** and **showing only essential information** to the user.

### 🟢 One‑Line Definition (Interview Version)
> **Abstraction is the concept of hiding internal implementation details and exposing only necessary features to the user. In Python, we achieve abstraction using abstract classes from the ABC module or interface-like behavior.**

---

## ⭐ 2. Why Abstraction? (Purpose)
Abstraction helps to:

✔ Reduce complexity  
✔ Improve security (hide internal logic)  
✔ Make code easier to use  
✔ Enforce structure in large systems  

---

## ⭐ 3. How Python Supports Abstraction
Python mainly provides two ways:

### **1. Abstract Classes**
- Created using `ABC` module
- Can contain:
  - abstract methods (no implementation)
  - normal methods (with implementation)
- Abstract methods act as a **contract**

### **2. Interfaces (Conceptually)**
Python does not have `interface` keyword like Java, but interface-like behavior can be achieved using:
- abstract classes with only abstract methods
- protocols (`typing.Protocol`, Python 3.8+)

---

## ⭐ 4. Real‑Life Example — ATM
User sees only:

- enter PIN  
- enter amount  
- withdraw cash  

Hidden details:

❌ authentication  
❌ balance check  
❌ backend updates  
❌ account validation  

These internal details are **abstracted away**.

---

## ⭐ 5. Programming Example — Payment System

Imagine an online payment system where users can pay using:

- Credit Card
- UPI
- Wallet

For the user, the important action is:

```python
user.pay()
```

Internal complexity like encryption, API calls, validation etc. is hidden.

To ensure every payment type must implement `pay()`, we create an abstract class:

```python
from abc import ABC, abstractmethod

class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

Now each child class must implement `pay()`:

```python
class UPI(Payment):
    def pay(self, amount):
        print("Paid using UPI")

class Wallet(Payment):
    def pay(self, amount):
        print("Paid using Wallet")
```

If a developer tries to create a payment class without `pay()`, Python throws:

```
TypeError: Can't instantiate abstract class ...
```

This **enforces structure** and makes the system safe.

---

## ⭐ 6. Benefit Summary
Abstraction provides:

✔ Cleaner system design  
✔ Enforced rules / contracts  
✔ Hidden complexity  
✔ Security of internal logic  
✔ Easier future extension  

---

## ⭐ 7. Difference Between Polymorphism & Abstraction (Simple Explanation)

### **1. Purpose**
| Concept | Purpose |
|---|---|
| **Abstraction** | Hide implementation details and show only necessary features |
| **Polymorphism** | Allow the same method to behave differently based on the object |

### **2. Method Requirement**
| Concept | Method Requirements |
|---|---|
| **Abstraction** | Child class **must** implement all abstract methods (else error) |
| **Polymorphism** | Methods do not need to be abstract; they just share the same name |

### **3. Behavior**
- **Polymorphism** → Same function name, different behavior depending on which object is calling it.
- **Abstraction** → Hides **how** the behavior is implemented.

### **Memory Trick**
➡ **Abstraction = WHAT to do** (contract)  
➡ **Polymorphism = HOW to do** (different behavior)

---

## ⭐ 8. Quick Code Showing Both Concepts Together

```python
from abc import ABC, abstractmethod

class Payment(ABC):        # Abstraction
    @abstractmethod
    def pay(self, amount):
        pass

class UPI(Payment):        # Polymorphism via overriding
    def pay(self, amount):
        print("Paid using UPI")

class Card(Payment):       # Polymorphism via overriding
    def pay(self, amount):
        print("Paid using Card")

# Polymorphism in action
for method in [UPI(), Card()]:
    method.pay(500)
```

Output:
```
Paid using UPI
Paid using Card
```

---

## ⭐ 9. Final Interview Summary

> **Abstraction hides implementation and exposes only required features. In Python, it is achieved using the `ABC` module and abstract methods. Polymorphism works with abstraction to provide different behavior for the same method name across different objects.**
