Hello everyone, welcome to the world of SOLID principles! These concepts will help you write clean, maintainable, and scalable code in your Angular applications. Let's dive into each principle with relatable examples.

## 🔹 S - Single Responsibility Principle (SRP)

**What it Means:** Each class should have only one reason to change, meaning it should only have one job or responsibility. This makes it easier to manage and understand your code.

**Example:** Let's create separate services for candidate registration and exam scheduling.

```typescript
// candidate-registration.service.ts
@Injectable({ providedIn: 'root' })
export class CandidateRegistrationService {
  register(candidate: Candidate) {
    console.log(`Candidate ${candidate.name} registered.`);
  }
}

// exam-scheduling.service.ts
@Injectable({ providedIn: 'root' })
export class ExamSchedulingService {
  schedule(candidate: Candidate, date: Date) {
    console.log(`Exam for ${candidate.name} set for ${date.toDateString()}.`);
  }
}
```

**Why It Matters:** Each service focuses on one task. If you need to modify the registration logic, you only need to update the `CandidateRegistrationService`, minimizing the risk of introducing bugs in other areas of your application.

### **Use Case:**

In a real-world scenario, consider a large educational platform where candidates register for exams. By having distinct services for registration and scheduling, you can easily adjust each process without interfering with the other. This makes testing and debugging more efficient.

---

## 🔹 O - Open/Closed Principle (OCP)

**What it Means:** Classes should be open for extension but closed for modification. You can add new functionality without changing existing code.

**Example:** Let’s extend a base class to create different types of pens.

```typescript
// pen.model.ts
export abstract class Pen {
  abstract write(): void;
}

// ballpen.service.ts
@Injectable({ providedIn: 'root' })
export class BallPenService extends Pen {
  write() {
    console.log('Writing with a ballpen.');
  }
}

// gelpen.service.ts
@Injectable({ providedIn: 'root' })
export class GelPenService extends Pen {
  write() {
    console.log('Writing with a gel pen.');
  }
}
```

**Why It Matters:** New pen types can be added without touching the base `Pen` class, ensuring stability. This reduces the chances of bugs since you’re not modifying existing, tested code.

### **Use Case:**

Imagine you want to add a new type of pen, like a fountain pen. You can simply create a new class `FountainPenService` extending `Pen`, without altering the existing functionality. This makes your application flexible and adaptable to change.

---

## 🔹 L - Liskov Substitution Principle (LSP)

**What it Means:** Subclasses should be replaceable with their parent class without altering the correctness of the program. This ensures that the derived class extends the behavior of the parent class.

**Example:** Different payment methods that can be used interchangeably.

```typescript
// payment-method.model.ts
export abstract class PaymentMethod {
  abstract pay(amount: number): void;
}

// cash-payment.service.ts
@Injectable({ providedIn: 'root' })
export class CashPaymentService extends PaymentMethod {
  pay(amount: number) {
    console.log(`Paid ₱${amount} with cash.`);
  }
}

// card-payment.service.ts
@Injectable({ providedIn: 'root' })
export class CardPaymentService extends PaymentMethod {
  pay(amount: number) {
    console.log(`Paid ₱${amount} with card.`);
  }
}
```

**Why It Matters:** Any payment method can be used where `PaymentMethod` is expected. This allows you to add new payment methods (like e-wallets) later without changing the code that processes payments.

### **Use Case:**

In a retail application, if a customer chooses to pay with cash or card, the system should handle both equally. If you replace `PaymentMethod` with either subclass, the application should function flawlessly, demonstrating true polymorphism.

---

## 🔹 I - Interface Segregation Principle (ISP)

**What it Means:** Create small, specific interfaces rather than one large, general interface. This avoids forcing classes to implement unnecessary methods.

**Example:** Separate interfaces for different cooking methods.

```typescript
// cooking-interfaces.ts
export interface Frying {
  fry(): void;
}

export interface Grilling {
  grill(): void;
}

// fry-cook.service.ts
@Injectable({ providedIn: 'root' })
export class FryCookService implements Frying {
  fry() {
    console.log('Frying chicken.');
  }
}

// grill-cook.service.ts
@Injectable({ providedIn: 'root' })
export class GrillCookService implements Grilling {
  grill() {
    console.log('Grilling burger.');
  }
}
```

**Why It Matters:** Services only implement the interfaces they need, leading to cleaner, more focused code. This reduces the implementation burden on classes and helps maintain separation of concerns.

### **Use Case:**

Imagine a restaurant application where cooks specialize in either frying or grilling. By defining specific interfaces, you ensure that fry cooks don’t need to worry about grilling methods and vice versa, enhancing code clarity and maintenance.

---

## 🔹 D - Dependency Inversion Principle (DIP)

**What it Means:** Depend on abstractions (interfaces) instead of concrete classes. This reduces coupling between components, making your system more flexible and easier to maintain.

**Example:** Using different delivery services without worrying about their specific implementations.

```typescript
//delivery-service.model.ts
export interface DeliveryService {
  deliver(orderId: number): void;
}

// lalamove.service.ts
@Injectable({ providedIn: 'root' })
export class LalamoveService implements DeliveryService {
  deliver(orderId: number) {
    console.log(`Delivering order ${orderId} with Lalamove.`);
  }
}

// grab.service.ts
@Injectable({ providedIn: 'root' })
export class GrabService implements DeliveryService {
  deliver(orderId: number) {
    console.log(`Delivering order ${orderId} with Grab.`);
  }
}
```

**Why It Matters:** Components can use any `DeliveryService` without knowing the specifics, promoting loose coupling. This makes it easier to swap out implementations without affecting the dependent components.

### **Use Case:**

In an e-commerce application, you might want to switch from using Lalamove to Grab for delivery. Thanks to DIP, you can simply replace the service instance without modifying the logic that handles order delivery, ensuring quick adaptability to changes in your business needs.

---

By embracing these SOLID principles in your Angular applications, you’ll create a codebase that’s not only easier to maintain and extend but also a joy to work with! Each principle contributes to a more organized, efficient, and robust application, making your development process smoother.

Thank you for reading!

# Links
[Hashnode Documentation](https://noesamae.hashnode.dev/activity-25-solid-principles-in-angular)
