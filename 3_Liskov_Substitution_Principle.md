
# 🔥 Liskov Substitution Principle (LSP) in Java

---

## ❓ Why (Why is it important?)

👉 Parent class ka object jaha expect hai, waha agar child class ka object dal do to program ka behavior same rehna chahiye. 
👉 If the child **breaks the promise** of the parent → it’s an **LSP violation**.

---

# 🚫 ❌ Without LSP (Violation Example)

```java
class Vehicle {
    void startEngine() {
        System.out.println("Engine started...");
    }
}

class Car extends Vehicle {
    @Override
    void startEngine() {
        System.out.println("Car engine started...");
    }
}

class Bicycle extends Vehicle {
    @Override
    void startEngine() {
        // ❌ Problem: Bicycle doesn't have an engine
        throw new UnsupportedOperationException("Bicycle has no engine!");
    }
}

public class LSPViolationDemo {
    public static void main(String[] args) {
        Vehicle car = new Car();
        car.startEngine();  
        // ✅ Output: Car engine started...

        Vehicle cycle = new Bicycle();
        cycle.startEngine();  
        // ❌ Runtime error: UnsupportedOperationException
    }
}
````

### 🖥️ **Output**

```
Car engine started...
Exception in thread "main" java.lang.UnsupportedOperationException: Bicycle has no engine!
```

👉 Here, **LSP is violated** because the parent class `Vehicle` promises that
`startEngine()` will work for all vehicles.
But **Bicycle broke the promise** → program crashed.

---

# ✅ With LSP (Correct Example)

👉 Solution: Design the parent-child hierarchy properly.

```java
// Base class for all vehicles
class Vehicle {
    void move() {
        System.out.println("I can move on road");
    }
}

// Only Engine-based vehicles
class EngineVehicle extends Vehicle {
    void startEngine() {
        System.out.println("Engine started...");
    }
}

// Car is an engine-based vehicle
class Car extends EngineVehicle {
    @Override
    void startEngine() {
        System.out.println("Car engine started...");
    }
}

// Bicycle is NOT engine-based, so it won't override startEngine
class Bicycle extends Vehicle {
    @Override
    void move() {
        System.out.println("Bicycle pedals forward...");
    }
}

public class LSPSatisfiedDemo {
    public static void main(String[] args) {
        Vehicle cycle = new Bicycle();
        cycle.move();  
        // ✅ Output: Bicycle pedals forward...

        EngineVehicle car = new Car();
        car.startEngine();  
        // ✅ Output: Car engine started...
    }
}
```

### 🖥️ **Output**

```
Bicycle pedals forward...
Car engine started...
```

---

## 🧠 Easy Summary

* 🚫 **Without LSP:** All vehicles were forced to have `startEngine()` → in case of Bicycle, this was a false promise → crash.
* ✅ **With LSP:** We separated hierarchy (EngineVehicle vs Vehicle) → now all child classes properly follow their parent’s behavior.

---
