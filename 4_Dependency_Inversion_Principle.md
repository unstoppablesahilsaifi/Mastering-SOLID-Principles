
# ⚡ **Dependency Inversion Principle (DIP)**  

---

## ❓ **Why (Kyun zaroori hai?)**  

👉 Normally hum **high-level classes** (business logic) ko **direct low-level classes** (implementation) pe depend kara dete hain.  
👉 Problem: Agar low-level class badal jaye, to high-level class bhi toot jaati hai.  

**DIP kehta hai:**  

1. High-level modules should not depend on low-level modules.  
2. Dono ko **abstractions (interfaces)** pe depend karna chahiye.  

---

## ❌ **Without DIP (Violation Example)**  

```java
// Low-level class
class Keyboard {
    void connect() {
        System.out.println("Keyboard connected");
    }
}

// High-level class (depends directly on Keyboard)
class Computer {
    private Keyboard keyboard;

    public Computer() {
        this.keyboard = new Keyboard(); // ❌ Tight coupling
    }

    void start() {
        keyboard.connect();
        System.out.println("Computer started...");
    }
}

public class DIPViolationDemo {
    public static void main(String[] args) {
        Computer pc = new Computer();
        pc.start();
    }
}
````

### 🖥️ **Output**

```
Keyboard connected
Computer started...
```

👉 **Problem:** Agar kal ko `Keyboard` ki jagah `WirelessKeyboard` ya `Mouse` use karna ho → `Computer` class modify karni pdegi.
🔴 Yaani high-level (Computer) dependent hai low-level (Keyboard) pe.

---

## ✅ **With DIP (Correct Example)**

👉 Ab abstraction (interface) introduce karte hain.

```java
// Abstraction
interface InputDevice {
    void connect();
}

// Low-level implementations
class Keyboard implements InputDevice {
    @Override
    public void connect() {
        System.out.println("Keyboard connected");
    }
}

class Mouse implements InputDevice {
    @Override
    public void connect() {
        System.out.println("Mouse connected");
    }
}

// High-level class depends on abstraction
class Computer {
    private InputDevice device;

    // Inject dependency via constructor
    public Computer(InputDevice device) {
        this.device = device;
    }

    void start() {
        device.connect();
        System.out.println("Computer started...");
    }
}

public class DIPSatisfiedDemo {
    public static void main(String[] args) {
        // Computer works with any input device now
        Computer pc1 = new Computer(new Keyboard());
        pc1.start();
        // Output: Keyboard connected + Computer started...

        Computer pc2 = new Computer(new Mouse());
        pc2.start();
        // Output: Mouse connected + Computer started...
    }
}
```

### 🖥️ **Output**

```
Keyboard connected
Computer started...
Mouse connected
Computer started...
```

---

## 🧠 **Easy Summary**

* **Without DIP:** High-level `Computer` class directly depends on `Keyboard`. Change in `Keyboard` → break `Computer`.
* **With DIP:** High-level `Computer` depends only on **abstraction** (`InputDevice`). Actual device (`Keyboard` / `Mouse`) inject hota hai → ✅ Flexible, ✅ Maintainable.

---

