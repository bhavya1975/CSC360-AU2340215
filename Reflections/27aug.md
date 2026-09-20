# Reflection: CI/CD, JAR Files, and Software Testing

## 1. JAR Files

A **JAR (Java Archive)** file is essentially a ZIP-like package used to distribute Java applications or libraries.

It can contain:

* Compiled Java **bytecode (`.class` files)**
* Resources such as configuration files
* Metadata
* Application information

For example:

```text
MyApplication.jar
├── Main.class
├── User.class
├── config.properties
└── META-INF/
```

A common misconception is that a JAR **always contains all its dependencies**. Normally, a JAR contains the application's own classes and resources, while external dependencies are handled separately.

Build tools such as **Maven** can download dependencies from public repositories and make them available during compilation and execution.

---

# 2. Continuous Integration (CI)

**Continuous Integration** is the practice of frequently integrating code changes into a shared repository and automatically verifying that the new code works.

A typical CI flow is:

```text
Developer
    |
    | Push code
    v
Central Repository
    |
    v
CI Server
    |
    v
Build / Compile
    |
    +---- Fail → Developer fixes the code
    |
    v
Automated Tests
    |
    +---- Fail → Developer investigates
    |
    v
Success
```

For example, when code is pushed to GitHub, a CI server can detect the change, obtain the latest source code, install the required dependencies, compile the project, and execute the automated tests.

The important idea is that **every change is automatically checked instead of waiting until the entire project is finished**.

---

# 3. Continuous Delivery and Continuous Deployment

After CI verifies the code, the next stage is concerned with getting the application ready for users.

### Continuous Delivery

The application is automatically **built and packaged into a deployable artifact** and made ready for release.

```text
Code
  ↓
Build
  ↓
Test
  ↓
Create Artifact
  ↓
Store Artifact
  ↓
Ready for Deployment
```

A human may still decide when to deploy it to production.

### Continuous Deployment

Continuous Deployment goes one step further.

After the build and tests succeed, the system **automatically deploys the new version to production**.

```text
Code Push
    ↓
Build
    ↓
Test
    ↓
Create Artifact
    ↓
Deploy to Production
    ↓
Restart / Reload Application
```

Therefore:

> **CI verifies the code. CD automates getting the verified code into a deployable or deployed state.**

The exact deployment process depends on the infrastructure. Modern systems may use containers, orchestration platforms, rolling deployments, or other techniques instead of simply restarting a web server.

---

# 4. Unit Testing and JUnit

**Unit testing** involves testing small, isolated pieces of an application, usually individual methods or classes.

In Java, **JUnit** is one of the most commonly used frameworks for writing and running unit tests.

For example, if we have:

```java
int add(int a, int b) {
    return a + b;
}
```

we can write a test that checks:

```text
add(2, 3) → expected result: 5
```

The advantage is that tests can be executed automatically whenever the project is built or changes are pushed.

This connects directly to CI:

```text
Code Change
    ↓
CI Build
    ↓
JUnit Tests
    ↓
Pass / Fail
```

---

# 5. Different Types of Testing

Unit testing is only one level of software testing.

### Unit Testing

Tests a small individual component.

**Example:**
Testing whether `calculateTotal()` returns the correct value.

### Integration Testing

Tests whether multiple components work correctly together.

**Example:**
Checking whether the application correctly communicates with a database.

### Black-Box Testing

In **black-box testing**, we test the system based on its inputs and outputs without needing to know its internal implementation.

```text
Input → [ System ] → Output
```

For example, we provide a username and password and check whether the application correctly allows or rejects the login.

The tester is concerned with **what the system does**, rather than how the code internally produces the result.

---

# 6. Testing a GUI

The same testing principles can be applied to graphical applications.

For example, instead of manually clicking every button every time we change the application, automated GUI testing can verify expected behavior.

A GUI test might check:

```text
Open application
      ↓
Click "Login"
      ↓
Enter username/password
      ↓
Click "Submit"
      ↓
Check expected screen/message
```

This becomes particularly useful as the application grows.

Manual testing might work for a small application, but repeatedly checking hundreds of existing features after every code change becomes slow and unreliable.

Automated tests provide a **repeatable safety net**.

---

# 7. Connecting Everything Together

The major connection between these topics is automation.

A developer makes a change:

```text
       Developer
           |
           v
     Push to Repository
           |
           v
          CI
           |
      +----+----+
      |         |
    Build     Tests
      |         |
      +----+----+
           |
         Pass
           |
           v
   Create JAR / Artifact
           |
           v
          CD
           |
           v
      Production
```

This creates a development pipeline where code is not merely written, but **automatically compiled, tested, packaged, and potentially deployed**.

## Key Reflection

The main takeaway is that modern software development relies heavily on **automation and continuous verification**. JAR files provide a way to package Java applications, JUnit allows individual pieces of code to be tested automatically, and CI/CD connects these processes into a pipeline.

Instead of discovering a problem only after manually deploying an application, the development pipeline tries to catch problems much earlier:

> **Write → Build → Test → Package → Deploy**

This reduces manual effort and makes software delivery more reliable and repeatable.
