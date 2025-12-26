
# Online Product Ordering System — OOPS Learning Example

## 🏷 Project Title
**Online Product Ordering System — OOPS Example (Beginner LLD Practice)**

## 📌 Objective
Understand how to approach an OOPS + Low Level Design problem by identifying:

1. Entities  
2. Attributes  
3. Methods/Behaviors  
4. Class responsibilities (SRP)  
5. Composition instead of dict  
6. Writing clean class-based code  

## 🔥 Problem Statement
Design a simple online order system.
A user should be able to order products, and the system must display ordered products with total price.

## 🧠 Clarification During Design Discussion
- Question asked: *Is this food ordering or product ordering?*
- Answer: Generic product ordering (store-like), only ordering + total cost.

## 🧱 System Design
### Entities
- Product
- Order

### Product Entity
**Attributes**
- product_name
- product_price

**Responsibility**
Stores product information only.

### Order Entity
**Attributes**
- order_products (list of Product objects)
- total_price

**Methods**
- add_product(product)
- show_order()

Order uses **composition (HAS-A)** relationship with Product.

## 🧠 SOLID Principle Applied
**Single Responsibility Principle (SRP)**  
Product = data only  
Order = handles order logic

## 💻 Final Code

```python
class Product:
    def __init__(self, product_name, product_price):
        if product_price < 0:
            raise ValueError("Price cannot be negative")
        self.product_name = product_name
        self.product_price = product_price


class Order:
    def __init__(self):
        self.order_products = []
        self.total_price = 0

    def add_product(self, product):
        self.order_products.append(product)
        self.total_price += product.product_price

    def show_order(self):
        print("Ordered Products:")
        for product in self.order_products:
            print(product.product_name, ":", product.product_price)
        print("Total Price:", self.total_price)


p1 = Product("Laptop", 50000)
p2 = Product("Keychain", 500)

order = Order()
order.add_product(p1)
order.add_product(p2)

order.show_order()
```

## 🧠 Key Learnings
- Product ≠ Order responsibility
- Pass **objects**, not dicts
- Composition is better here
- SRP applied naturally
- User interacts with Order only

## Interview Summary
> Product holds data. Order manages ordering behavior and calculates total.
> This follows SRP and composition.

## Next Learning Step
👉 Move to **Inheritance** next.  
