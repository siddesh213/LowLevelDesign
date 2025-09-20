
# DRY Principle (Scratch → Advanced) & Parking Lot System Example

---

## 🔹 Step 1: What is DRY? (Definition + Example)

**Definition (simple words):**  
DRY means don’t write the same logic more than once. Write it in one place and reuse it everywhere.

**Real-life Example:**  
Imagine you write your phone number on 10 different forms. Tomorrow, your number changes. Now you must update all 10 forms → painful.  
Instead, you could just write it once in your ID card and tell everyone to refer there.

**Code Example:**

❌ Without DRY:
```python
def get_area_of_square(side):
    return side * side

def print_square_area(side):
    print("Area:", side * side)  # repeated logic
```

✅ With DRY:
```python
def get_area_of_square(side):
    return side * side

def print_square_area(side):
    print("Area:", get_area_of_square(side))  # reused
```

👉 Logic written once. If formula changes, update in one place only.

---

## 🔹 Step 2: When to Apply DRY?

**Rule:** If you see yourself copy-pasting code → stop. That’s the moment to apply DRY.

**Real-life Example:**  
Think about school homework. Instead of copying the same multiplication table on 10 pages, you write it once and say: “This applies for all.”

**Code Example:**

❌ Without DRY:
```python
# User registration
if "@" not in email or len(password) < 6:
    print("Invalid input")

# User login
if "@" not in email or len(password) < 6:
    print("Invalid input")
```

✅ With DRY:
```python
def validate_user(email, password):
    return "@" in email and len(password) >= 6

# User registration
if not validate_user(email, password):
    print("Invalid input")

# User login
if not validate_user(email, password):
    print("Invalid input")
```

👉 Now, validation logic is one place only.

---

## 🔹 Step 3: Where to Apply DRY?

Apply DRY in common, repeating logic like:

- Calculations  
- Validations  
- Logging  
- Configuration  
- Database queries  

**Real-life Example:**  
In Amazon, “delivery charges calculation” is common for cart, checkout, and order summary. If you repeat it everywhere → nightmare.

**Code Example (Amazon-style):**

❌ Without DRY:
```python
class Cart:
    def calculate_delivery_fee(self, distance):
        if distance < 5: return 20
        else: return 50

class Order:
    def calculate_delivery_fee(self, distance):
        if distance < 5: return 20
        else: return 50
```

✅ With DRY:
```python
class DeliveryFeeCalculator:
    @staticmethod
    def calculate(distance):
        if distance < 5: return 20
        else: return 50

class Cart:
    def calculate_delivery_fee(self, distance):
        return DeliveryFeeCalculator.calculate(distance)

class Order:
    def calculate_delivery_fee(self, distance):
        return DeliveryFeeCalculator.calculate(distance)
```

👉 One place → less headache.

---

## 🔹 Step 4: What if You Don’t Apply DRY? (Impact)

**Real-life Example:**  
Your teacher changes multiplication table logic (say from base 10 to base 12 😅).  
If you wrote it on 20 pages, you must erase all → waste of time.

**Impact in Coding:**

- Bugs (forgetting to change in one place)  
- Wasted time  
- Hard to scale  

**Code Example:**

❌ Without DRY:
```python
# In 3 different files
total = price * qty * 1.18   # hard-coded GST
```

Now GST changes → you must update in all 3 files. If you miss one, your app gives wrong results.

✅ With DRY:
```python
GST = 1.18

def calculate_total(price, qty):
    return price * qty * GST
```

👉 One change updates everywhere.

---

## 🔹 Step 5: Advantages of DRY

- Easier maintenance  
- Reusable code  
- Cleaner design (interviewer loves this)  
- Fewer bugs  

**Real-life Example:**  
Think of a Google Doc → you update one file, everyone sees the update.  
Instead of sending 10 copies and updating each.

**Code Example:**  
Without DRY → you write tax calculation in Cart, Order, Invoice separately.  
With DRY → you write once in `TaxCalculator`.

---

# Parking Lot System – Step by Step Approach (With DRY)

---

## Step 0: Understand the Problem (Clarify Requirements)

**Interviewer asks:**  
“Design a Parking Lot system. Users can park vehicles (Car, Bike, Truck). System should generate tickets, track vehicles, and calculate fees.”

**Questions to Clarify:**

- How many vehicle types? (Car, Bike, Bus)  
- How is the fee calculated? Fixed or dynamic?  
- Is there a limit on parking slots?  
- Should it handle entry/exit time?  

**Always think:** “I want clear inputs, outputs, and constraints.”

---

## Step 1: Identify Classes (Think in terms of objects)

Speak aloud:

> “From the requirements, I see these objects:
>
> - ParkingLot → main system  
> - Vehicle → base class for Car, Bike, Truck  
> - ParkingSlot → represents a parking spot  
> - Ticket → holds info about parking, time, fee  
> - FeeCalculator → calculates fees (important for DRY)”

✅ Key point: think in terms of **reusability and DRY**.

---

## Step 2: Identify Repeated Logic (Where DRY applies)

Speak aloud:

> “I notice some logic can be repeated:
>
> - Fee calculation for different vehicles  
> - Ticket generation  
> - Validation (e.g., check if a slot is free)”

> “These can be extracted into reusable components instead of copying in multiple classes.”

---

## Step 3: Define Classes Using DRY

### FeeCalculator + Vehicle
```python
class FeeCalculator:
    @staticmethod
    def calculate(vehicle_type, hours):
        if vehicle_type == "Car":
            base, extra = 20, 10
        elif vehicle_type == "Bike":
            base, extra = 10, 5
        elif vehicle_type == "Bus":
            base, extra = 50, 25
        else:
            raise ValueError("Invalid vehicle type")
        
        if hours <= 2:
            return base
        else:
            return base + (hours - 2) * extra

class Vehicle:
    def __init__(self, vehicle_type, hours):
        self.vehicle_type = vehicle_type
        self.hours = hours

    def calculate_fee(self):
        return FeeCalculator.calculate(self.vehicle_type, self.hours)
```

**Explain to interviewer:**  
> “Instead of writing fee calculation inside Car, Bike, Truck separately, I created a static `FeeCalculator`.  
> Now all vehicle types reuse it. This is **DRY principle in action**. If Amazon changes the fee rule tomorrow, I update only in one place.”

---

### Ticket Generation
```python
class Ticket:
    ticket_counter = 0

    @staticmethod
    def generate(vehicle, slot_id):
        Ticket.ticket_counter += 1
        return f"TICKET-{Ticket.ticket_counter}-{vehicle.vehicle_type}-Slot{slot_id}"
```

---

### ParkingLot Class
```python
class ParkingLot:
    def __init__(self, car_slots, bike_slots, bus_slots):
        self.available_slots = {"Car": car_slots, "Bike": bike_slots, "Bus": bus_slots}
        self.occupied_slots = {"Car": [], "Bike": [], "Bus": []}

    def park_vehicle(self, vehicle):
        v_type = vehicle.vehicle_type
        if self.available_slots[v_type] <= 0:
            print(f"No {v_type} slots available!")
            return None

        slot_id = len(self.occupied_slots[v_type]) + 1
        self.occupied_slots[v_type].append(vehicle)
        self.available_slots[v_type] -= 1

        ticket = Ticket.generate(vehicle, slot_id)
        fee = vehicle.calculate_fee()
        print(f"{v_type} parked at slot {slot_id}, Ticket: {ticket}, Fee: {fee}")
        return ticket
```

---

### Step 4: Test Parking Lot System
```python
# Create parking lot
parking_lot = ParkingLot(car_slots=5, bike_slots=3, bus_slots=2)

# Park vehicles
v1 = Vehicle("Car", 3)
v2 = Vehicle("Bike", 1)
v3 = Vehicle("Bus", 4)

parking_lot.park_vehicle(v1)
parking_lot.park_vehicle(v2)
parking_lot.park_vehicle(v3)
```

**Expected Output:**  
```
Car parked at slot 1, Ticket: TICKET-1-Car-Slot1, Fee: 30
Bike parked at slot 1, Ticket: TICKET-2-Bike-Slot1, Fee: 10
Bus parked at slot 1, Ticket: TICKET-3-Bus-Slot1, Fee: 75
```

---

## ✅ Key Takeaways

- DRY = write once, reuse everywhere  
- Centralize repeating logic like **fees, validation, ticket generation**  
- Makes code **maintainable, scalable, and bug-free**  
- Always **think aloud** in interviews and show **how DRY applies**  
