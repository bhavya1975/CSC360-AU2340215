# Class Reflection: 20-Aug-2026

---

## `.md` Explanation

In this lecture, we learnt how to make a `.md` file in a better and more optimized way.

Sir taught us different types of symbols like `#`, `---`, and how we can use them in a more desired and better way.

---

## User Convenience

When a user wants to run the `Square` class to get the square drawn, we can do this with `args[]`.

So, when the user simply runs:

`./square`

we throw the usage information showing which parameters need to be passed to get the expected output.

Hence, usage is a must.

---


## Jframes

- `JFrame` creates a window, and inbuilt java class with subclass implementation let us do it easily.
- we runtime polymorphism(override) `paint()` by `super.paint()` calls the parent class, that allows us to do whatever we want.

## How to Make the Subclass Inline

```java
X x = new X() {
    // implementation
};

