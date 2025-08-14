# 📜 Open/Closed Principle (OCP)

Let’s understand **O – Open/Closed Principle (OCP)**

---

## 1️⃣ Why is it Needed?

Software always requires **maintenance** and **enhancements**:

* Adding new features
* Modifying old code

If you have to **modify existing classes for every new requirement**:

* ❌ Risk increases, bugs appear
* ❌ Testing load increases
* ❌ Code becomes brittle (easy to break)

**Solution → Open/Closed Principle:**

* ✅ **Open for extension** → you can add new features
* ✅ **Closed for modification** → existing tested code does not need to change

---

## 2️⃣ What is it?

📖 **Definition (Robert C. Martin):**

> “Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.”

**In simple words:**

* Do **not change** the old class
* Add **new functionality** by creating **new classes that extend** existing ones

---

## 3️⃣ Without OCP – What Happens?

#### Example: Discount Calculator

```java
// Without OCP - Every new discount type requires class modification
class DiscountCalculator {
    public double calculate(String customerType, double price) {
        if(customerType.equals("Regular")) {
            return price * 0.9; // 10% discount
        } else if(customerType.equals("Premium")) {
            return price * 0.8; // 20% discount
        } else {
            return price; // no discount
        }
    }

    public static void main(String[] args) {
        DiscountCalculator calculator = new DiscountCalculator();
        System.out.println("Regular: " + calculator.calculate("Regular", 1000));
        System.out.println("Premium: " + calculator.calculate("Premium", 1000));
    }
}
```

⚠ **Problems Without OCP:**

1. Every change breaks tested code → adding a new discount type requires modifying existing methods
2. Code is not scalable → `if-else` grows with each new customer type
3. Hard to maintain & extend → new requirements break old code

---

## 4️⃣ After OCP – What Happens?

Following OCP:

* Create a **base class/interface**
* Add **subclass/implementation** for new functionality
* Existing code **does not need to be touched**

#### Code Example With OCP:

```java
// 1. Base Interface
interface Discount {
    double calculate(double price);
}

// 2. Regular customer discount
class RegularDiscount implements Discount {
    public double calculate(double price) {
        return price * 0.9; // 10% discount
    }
}

// 3. Premium customer discount
class PremiumDiscount implements Discount {
    public double calculate(double price) {
        return price * 0.8; // 20% discount
    }
}

// 4. New VIP customer discount can be added without changing existing code
class VIPDiscount implements Discount {
    public double calculate(double price) {
        return price * 0.7; // 30% discount
    }
}

// 5. Calculator uses interface
class DiscountCalculatorOCP {
    public double calculate(Discount discountStrategy, double price) {
        return discountStrategy.calculate(price);
    }

    public static void main(String[] args) {
        DiscountCalculatorOCP calculator = new DiscountCalculatorOCP();

        Discount regular = new RegularDiscount();
        Discount premium = new PremiumDiscount();
        Discount vip = new VIPDiscount();

        System.out.println("Regular: " + calculator.calculate(regular, 1000));
        System.out.println("Premium: " + calculator.calculate(premium, 1000));
        System.out.println("VIP: " + calculator.calculate(vip, 1000));
    }
}
```

---

## ✅ Benefits With OCP

1. ✅ Open for extension → add new discount types
2. ✅ Closed for modification → existing classes remain safe
3. ✅ Easy maintenance & scalability → adding new features is simple
4. ✅ Clean & readable → no `if-else` jungle
5. ✅ Better testing → each strategy can have its own unit test

---

## 💡 Real-life Analogy

* **Without OCP:** Every new button on a TV remote breaks the old remote
* **With OCP:** You design a **universal remote** where **new buttons can be plugged in**, keeping the old remote safe

---

## 📌 OCP Summary

> **“Do not touch existing code; add extensions for new features.”**

---
