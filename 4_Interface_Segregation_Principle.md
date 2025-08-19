
# 🔥 **Interface Segregation Principle (ISP)**

---

## ❓ **Why (Kyun zaroori hai?)**


👉 Agar ek **bada interface** bana diya jisme unnecessary methods hain, to **client classes ko un methods ko implement karna padta hai jinki unko zaroorat hi nahi**.  
👉 Ye hi violation hai → **fat interfaces = problem**.

**ISP kehta hai:**  

> ⚡ Clients should not be forced to depend on methods they do not use.  
> 🪶 (Chhote-chhote specific interfaces banao, unnecessary burden mat do.)

---

## ❌ **Without ISP (Violation Example)**

```java
// Bad interface: Too many methods
interface Worker {
    void work();
    void eat();
}

class HumanWorker implements Worker {
    @Override
    public void work() {
        System.out.println("Human is working...");
    }

    @Override
    public void eat() {
        System.out.println("Human is eating...");
    }
}

class RobotWorker implements Worker {
    @Override
    public void work() {
        System.out.println("Robot is working...");
    }

    @Override
    public void eat() {
        // ❌ Problem: Robot doesn't eat, but still forced to implement
        throw new UnsupportedOperationException("Robot doesn't eat!");
    }
}

public class ISPViolationDemo {
    public static void main(String[] args) {
        Worker human = new HumanWorker();
        human.work(); // ✅ Human is working...
        human.eat();  // ✅ Human is eating...

        Worker robot = new RobotWorker();
        robot.work(); // ✅ Robot is working...
        robot.eat();  // ❌ Runtime crash!
    }
}
````

### 🖥️ **Output**

```
Human is working...
Human is eating...
Robot is working...
Exception in thread "main" java.lang.UnsupportedOperationException: Robot doesn't eat!
```

👉 **Violation**: Robot ko `eat()` implement karna pada jo uske liye irrelevant hai.

---

## ✅ **With ISP (Correct Example)**

👉 Interfaces ko chhote aur specific bana dete hain.

```java
// Small and specific interfaces
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

// Human does both work and eat
class HumanWorker implements Workable, Eatable {
    @Override
    public void work() {
        System.out.println("Human is working...");
    }

    @Override
    public void eat() {
        System.out.println("Human is eating...");
    }
}

// Robot only works, no need to eat
class RobotWorker implements Workable {
    @Override
    public void work() {
        System.out.println("Robot is working...");
    }
}

public class ISPSatisfiedDemo {
    public static void main(String[] args) {
        Workable human = new HumanWorker();
        human.work();  // ✅ Human is working...

        Eatable eater = new HumanWorker();
        eater.eat();   // ✅ Human is eating...

        Workable robot = new RobotWorker();
        robot.work();  // ✅ Robot is working...
    }
}
```

### 🖥️ **Output**

```
Human is working...
Human is eating...
Robot is working...
```

---

## 🧠 **Easy Summary**

* 🚫 **Without ISP:**

  * Ek hi bada `Worker` interface bana diya → Robot ko `eat()` method implement karna pada jo uske liye irrelevant tha.

* ✅ **With ISP:**

  * `Workable` aur `Eatable` alag interfaces → ab classes sirf wahi methods implement karti hain jo unko chahiye.
  * ✅ No runtime crash
  * ✅ Clean design




---
