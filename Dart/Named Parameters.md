In **Dart**, curly brackets `{}` are mainly used for **named parameters** — a different style from positional parameters.

Here’s the full explanation:

---

# ✅ **1. Named parameters use `{}`**

When defining a function, curly brackets make the parameters **named**, meaning you specify them by name when calling the function.

### Example:

```dart
void greet({required String name, int age = 18}) {
  print("Hello $name, age $age");
}
```

Calling the function:

```dart
greet(name: "Kevin");
greet(name: "Kevin", age: 20);
```

### Why use named parameters?

- They make the function call more readable.
    
- Order does **not** matter.
    
- You can make some parameters optional or required.
    

---

# ✅ **2. Curly brackets for function bodies**

Every function, class, or control statement uses `{}` for its **block of code**:

```dart
void main() {
  print("Hello");
}

if (true) {
  print("Yes");
}
```

This is Dart’s way of grouping statements.

---

# ✅ **3. Curly brackets for Sets**

Dart uses `{}` to represent **Sets**:

```dart
var numbers = {1, 2, 3};
```

---

# 🎯 Summary

|Use Case|Example|
|---|---|
|**Named parameters**|`void f({int a, int b}) {}`|
|**Code blocks**|`if (...) { ... }`|
|**Set literals**|`{1, 2, 3}`|

---

If you want, I can show side-by-side examples of positional `[]` vs named `{}` parameters in Dart.