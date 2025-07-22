# **Encapsulation in Object-Oriented Programming (OOP)**

## ✅ What is Encapsulation?
- Encapsulation is one of the four fundamental concepts of OOP (Object-Oriented Programming).
- It refers to **binding data and methods** that operate on the data into a single unit called a **class**.
- It **restricts direct access** to some components of an object, which is a way of preventing unintended interference and misuse of data.
- Encapsulation improves **data protection**, **code modularity**, and **code maintenance**.

---

## 💡 Simple Real-Life Analogy
- Think of a capsule – it holds medicine inside. Just like that, a class encapsulates data and logic.
- You **interact with a capsule externally**, but the internal working is hidden.

---

## 🔐 Why is Encapsulation Important?
- Prevents unwanted access and modifications to internal data.
- Allows control over the data by using **methods (getters/setters)**.
- Increases code security and flexibility.
- Makes code easier to maintain and refactor.

---

## 🔍 Requirement & Use-Case Example (Banking System)
> In a real-world banking system:

- You **don’t want users to directly change the account balance** to a negative value.
- You want users to **interact using rules**, such as **only depositing or withdrawing valid amounts**.
- There should be **checks and balances** to maintain **data consistency** and **security**.

Encapsulation ensures these requirements are met by:
- Restricting direct access to sensitive data (like balance).
- Allowing access only through proper methods (like deposit, withdraw).

---

## 🧩 Public vs Private in Encapsulation
| Modifier | Access Level              | Use-Case                                               |
|----------|---------------------------|--------------------------------------------------------|
| `public` | Accessible from anywhere  | When data/methods are safe to expose to outside world. |
| `private`| Accessible only in class  | When data/methods must be hidden/protected.            |

---

## ❌ Without Encapsulation (Unsafe Example)
```python
class BankAccount:
    def __init__(self, holder_name, balance):
        self.holder_name = holder_name
        self.balance = balance  # ❌ Public

    def display_account(self):
        return f"Account Holder: {self.holder_name}, Balance: ₹{self.balance}"

# ❌ Usage
account = BankAccount("Siddesh", 1000)
print(account.display_account())

# ⚠️ Dangerous: Directly changing balance without any checks
account.balance = -5000
print(account.display_account())
```
**Output:**
```
Account Holder: Siddesh, Balance: ₹1000
Account Holder: Siddesh, Balance: ₹-5000
```
> 🛑 This is unsafe! It allows direct and invalid access to sensitive data.

---

## ✅ With Encapsulation (Safe Design)
```python
class BankAccount:
    def __init__(self, holder_name, balance):
        self.holder_name = holder_name
        self.__balance = balance  # ✅ Private

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount

    def display_account(self):
        return f"Account Holder: {self.holder_name}, Balance: ₹{self.__balance}"

# ✅ Usage
account = BankAccount("Siddesh", 1000)
account.deposit(500)
account.withdraw(200)
print(account.display_account())
```
**Output:**
```
Account Holder: Siddesh, Balance: ₹1300
```
> ✅ Now the balance is protected and can only be changed through controlled methods.

---

## ✅ Benefits Recap
- 🛡️ **Security** – Sensitive data is hidden.
- 🧩 **Modularity** – Code is clean and organized.
- 🛠️ **Maintainability** – Changes to implementation don’t affect external code.
- 🔍 **Control** – Data access is regulated and validated.

---

## 📌 Summary
Encapsulation is a critical OOP principle that ensures:
- Only **intended operations** can be performed on data.
- Internal object logic is hidden.
- System becomes **robust, secure, and scalable**.
