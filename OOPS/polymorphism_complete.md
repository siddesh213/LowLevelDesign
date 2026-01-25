# Polymorphism in Python --- Complete Guide

## 1. What is Polymorphism?

Polymorphism means **one interface, many implementations**. In simple
words, the **same method name behaves differently** depending on the
object.

Example meaning: \> `pay()` for UPI behaves differently than `pay()` for
CreditCard.

------------------------------------------------------------------------

## 2. Why Polymorphism Exists?

Polymorphism gives: - Flexibility - Extensibility - Code reusability -
Cleaner architecture - Reduced `if-else` checks - Supports **Open-Closed
Principle (SOLID)**

------------------------------------------------------------------------

## 3. Real-World Example --- Payment System

In an e-commerce platform, users can pay using: - UPI - Wallet - Credit
Card - COD (Cash On Delivery)

All of them share one action: \> `pay()`

But each executes **different logic**.

### Without Polymorphism (Bad)

Using `if-else`:

``` python
method = "upi"

if method == "upi":
    print("UPI Payment")
elif method == "card":
    print("Card Payment")
elif method == "wallet":
    print("Wallet Payment")
```

Problems: ❌ Hard to scale\
❌ Violates Open-Closed Principle\
❌ Add new method → modify old code

### With Polymorphism (Good)

``` python
class Payment:
    def pay(self):
        pass

class UPI(Payment):
    def pay(self):
        print("UPI Payment")

class Card(Payment):
    def pay(self):
        print("Card Payment")

class Wallet(Payment):
    def pay(self):
        print("Wallet Payment")

def checkout(payment_obj):
    payment_obj.pay()

checkout(UPI())
checkout(Card())
checkout(Wallet())
```

Benefits: ✔ No conditions\
✔ Easy extension (add new class only)\
✔ Clean design

------------------------------------------------------------------------

## 4. Types of Polymorphism in Python

### **4.1 Method Overriding (Runtime Polymorphism)**

Child class redefines parent's method.

``` python
class Animal:
    def sound(self):
        print("Generic sound")

class Dog(Animal):
    def sound(self):
        print("Bark")

class Cat(Animal):
    def sound(self):
        print("Meow")

for a in [Dog(), Cat()]:
    a.sound()
```

Output:

    Bark
    Meow

✔ Same method name, different behavior\
✔ Selected at **runtime**

------------------------------------------------------------------------

### **4.2 Duck Typing (Python-Specific)**

No inheritance required. If an object has the method, it works.

``` python
class Dog:
    def sound(self): print("Bark")

class Cat:
    def sound(self): print("Meow")

def make_sound(obj):
    obj.sound()

make_sound(Dog())
make_sound(Cat())
```

✔ Focus on **behavior**, not type

------------------------------------------------------------------------

### **4.3 Operator Polymorphism**

`+` works differently based on type:

``` python
print(1 + 2)
print("a" + "b")
print([1] + [2])
```

Outputs:

    3
    ab
    [1, 2]

------------------------------------------------------------------------

### **4.4 Built‑in Function Polymorphism**

`len()` works on different objects:

``` python
len("Hello")
len([1,2,3])
len({1:"a",2:"b"})
```

------------------------------------------------------------------------

## 5. Inheritance + Polymorphism Connection

Polymorphism works because of inheritance: - **Inheritance** → gives
relationship - **Overriding** → changes behavior - **Runtime
polymorphism** → decides which method to call

Duck typing is the **only exception** that doesn't need inheritance.

------------------------------------------------------------------------

## 6. 7‑Step Learning Flow (Our Roadmap)

1.  Definition\
2.  Types of polymorphism\
3.  Inheritance + polymorphism connection\
4.  Practical examples\
5.  When to use polymorphism\
6.  When NOT to use polymorphism\
7.  Real-world LLD use-cases

------------------------------------------------------------------------

## 7. When to Use Polymorphism (Very Important)

Use when: ✔ Same action, different behavior\
✔ Avoiding if‑else / switch chains\
✔ New types will be added later\
✔ Follows Open‑Closed Principle\
✔ Extensible system design

Best real use cases: - Payments - Notifications (Email, SMS, Push) -
File Export (PDF, Excel, CSV) - Database Drivers (MySQL, PostgreSQL) -
Strategy Pattern - Game character actions - Device drivers

Example:

``` python
notifier.send()
```

can work for: - EmailNotifier - SMSNotifier - PushNotifier

------------------------------------------------------------------------

## 8. When NOT to Use Polymorphism (Very Important)

Avoid polymorphism when:

❌ **No IS‑A relationship** Example: `Car(Engine)` → wrong (Car has
Engine, not Car is Engine)

❌ **Simple if‑else is enough** Example: Classifying age → no need for
polymorphism

❌ **Behavior won't change or grow** Example: Temperature conversion is
arithmetic, not types

❌ **Composition is better than inheritance** Use `HAS‑A` instead of
`IS‑A`

❌ **Will over-engineer the system** Example: Creating classes for
Celsius/Fahrenheit for basic math → too much

❌ **Performance critical code** Direct function calls are faster

------------------------------------------------------------------------

## 9. Overloading vs Overriding Comparison (Python View)

  Feature               Overloading           Overriding
  --------------------- --------------------- ------------------------
  Supported in Python   ❌ No (not true)      ✔ Yes
  Polymorphism          ❌ Compile-time       ✔ Runtime
  Method Name           Same                  Same
  Parameters            Different             Same
  Inheritance Needed    No                    Yes
  Use Case              Use `*args` instead   Change parent behavior

------------------------------------------------------------------------

## 10. Interview Q&A

**Q1: What is polymorphism?**\
A: Polymorphism allows the same interface or method name to behave
differently based on the object type.

**Q2: Types of polymorphism in Python?**\
- Method overriding - Duck typing - Operator polymorphism - Built‑in
polymorphism

**Q3: Overloading vs Overriding?**\
Python does not support true overloading, overriding is runtime behavior
change.

**Q4: Why polymorphism?**\
Supports scalability, Open‑Closed principle, and cleaner architecture.

**Q5: When NOT to use polymorphism?**\
When no IS‑A relationship, simple logic, or composition is better.

**Q6: Real LLD example?**\
Payment gateway with UPI, Wallet, Card where each overrides `pay()`.

------------------------------------------------------------------------

## 11. Final Interview Summary (Short Answer)

> Polymorphism lets the same method behave differently depending on the
> object. In Python, it mainly happens through method overriding, duck
> typing, operator polymorphism, and built‑in functions, enabling
> scalable and clean system design.
