**Inheritance** in Dart (and in OOP in general) is when one class **takes on** the properties and behavior of another class.

It lets you create a new class based on an existing class **without rewriting the same code**.

---

# ✅ Simple explanation

Think of inheritance like a _parent → child_ relationship:

- The **parent class** (also called _superclass_) has some fields and methods.
    
- The **child class** (also called _subclass_) _inherits_ them and can:
    
    - use them,
        
    - add more features,
        
    - or change how they work.
        

---

# ✅ Example

### Parent class (superclass)

```dart
class Animal {
  void eat() {
    print("Animal is eating");
  }
}
```

### Child class (subclass)

```dart
class Dog extends Animal {
  void bark() {
    print("Dog is barking");
  }
}
```

### Using them

```dart
void main() {
  var d = Dog();
  d.eat();   // inherited from Animal
  d.bark();  // Dog's own method
}
```

The `Dog` class **inherits** the `eat()` method from `Animal`.

---

# ✅ Why inheritance is useful

- Avoid writing duplicate code
    
- Organize related classes
    
- Extend old classes with new features
    
- Model “is-a” relationships
    
    - Dog **is an** Animal
        
    - Student **is a** Person
        

---

# 🔑 Keywords to know

- `extends` → used for inheritance
    
- `super` → refers to the parent class
    

Example:

```dart
class Vehicle {
  Vehicle() {
    print("Vehicle created");
  }
}

class Car extends Vehicle {
  Car() : super() {
    print("Car created");
  }
}
```

---

# 🎯 Quick definition to remember

> **Inheritance allows one class to borrow and extend the code of another class.**

---

If you want, I can explain:

- `super`
    
- overriding methods
    
- abstract classes
    
- mixins  
    or help you build real examples for your own app.