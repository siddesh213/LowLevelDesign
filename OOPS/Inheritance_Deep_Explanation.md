# Inheritance in OOP (Python) — README

## 1. What is Inheritance?
Inheritance is a process in OOP where one class (child/subclass) acquires the properties and behavior of another class (parent/superclass).

**Simple definition:**  
> Child class **is-a** Parent class.

Example:
```python
class Vehicle:
    pass

class Car(Vehicle):
    pass
```

---

## 2. Why do we use Inheritance?

Inheritance is mainly useful for:

### ✔ a) Code Reusability
Common attributes and methods live in the parent class, avoiding duplication.

### ✔ b) Establishing IS-A Relationship
Represents real-world hierarchical relationships.

### ✔ c) Easier Maintenance
Updates to base functionality automatically propagate to subclasses.

---

## 3. When to Use Inheritance?

Use inheritance **only** when the subclass truly **is a type of** the parent.

Examples:
- Car **is a** Vehicle → ✔ Valid
- Truck **is a** Vehicle → ✔ Valid

So design:
```
Vehicle
 ├── Car
 └── Truck
```

---

## 4. When *Not* to Use Inheritance?

If the relationship is **has-a**, not **is-a**.

Example:
- Car **has an** Engine (NOT Car is an Engine)
So use **composition**, not inheritance:
```python
class Car:
    def __init__(self):
        self.engine = Engine()  # Composition
```

---

## 5. Multiple Inheritance

Multiple inheritance means a class inherits from **more than one** parent.

Definition:
```python
class Child(Parent1, Parent2):
    pass
```

Use multiple inheritance when **both** IS-A relationships are valid.

Example:
```
SmartPhone → is a Phone
SmartPhone → is a Camera
```
So:
```python
class SmartPhone(Phone, Camera):
    pass
```

### ❗ When NOT to use multiple inheritance:
If only one or none IS-A relationships exist.

Example (invalid):
```
Car is a Vehicle ✔
Car is an Engine ❌
```
So this is **wrong**:
```python
class Car(Vehicle, Engine):  # ❌ Invalid design
    pass
```

---

## 6. How Python Handles Multiple Inheritance? → MRO

Python uses **MRO (Method Resolution Order)** to decide which parent to look at first.

Check MRO using:
```python
print(ClassName.__mro__)
```

Example MRO:
```
C → A → B → object
```

### Key rule:
> `super()` calls the next class in the **MRO chain**, not always the direct parent class.

---

## 7. `super()` Keyword

`super()` is used to call the next method in the MRO.

Example:
```python
class Vehicle:
    def info(self):
        print("Vehicle")

class Car(Vehicle):
    def info(self):
        super().info()
        print("Car")
```

Output:
```
Vehicle
Car
```

---

## 8. Valid Inheritance Decision Framework

When solving OOPS/LLD problems:

1. Identify entities (nouns)
2. Check IS-A relationships
3. If **IS-A once** → Single inheritance
4. If **IS-A twice** → Multiple inheritance
5. If **HAS-A** → Composition

---

## 9. Summary Table

| Situation | Relationship | Use |
|---|---|---|
| A is a B | IS-A | Inheritance |
| A is a B and A is a C | Multiple IS-A | Multiple Inheritance |
| A has a B | HAS-A | Composition |
| A uses B | Dependency | No inheritance |

---

## 10. Example Code (Multiple Inheritance)

```python
class Machine:
    def info(self):
        print("Machine")

class Vehicle(Machine):
    def info(self):
        print("Vehicle")
        super().info()

class Appliance(Machine):
    def info(self):
        print("Appliance")
        super().info()

class SmartVehicle(Vehicle, Appliance):
    def info(self):
        print("SmartVehicle")
        super().info()

obj = SmartVehicle()
obj.info()
```

### Output:
```
SmartVehicle
Vehicle
Appliance
Machine
```

---

## Final Notes

✔ Inheritance enables hierarchical modeling.  
✔ Multiple inheritance should be used carefully.  
✔ Always validate **IS-A** relationships.  
✔ Use **composition** for **HAS-A** relationships.  
✔ Python uses **MRO** to resolve method order.
