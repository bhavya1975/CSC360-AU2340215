# Class Reflection: GUI, Threads and Java Build Process

## Key Concepts Discussed

### 1. Upstream and Downstream

Upstream refers to where data or dependencies come from, while downstream refers to where they go. This helped me understand the flow of information between different components of a system.

### 2. `pom.xml` and `javac`

`pom.xml` is used by Maven to define the project's dependencies and build configuration. Maven uses compiler plugins and configuration from `pom.xml` to communicate with the Java compiler (`javac`).

The basic flow is:

`Java Code → Maven → javac → Bytecode (.class) → JVM`

This made me understand that Maven does not replace `javac`; it manages and coordinates the build process.

### 3. Accessibility

Accessibility means designing software so that it can be used by people with different abilities. In GUI applications, this includes things such as keyboard navigation, proper labels, and screen-reader support.

### 4. Thread Safety

A major discussion was about multiple people accessing the same "bag". If two people try to write to the same bag at the same time, the final result may become unpredictable.

Similarly, in software, when multiple threads access and modify the same data, we can get **race conditions**.

Even reading can become problematic if another thread changes the data while it is being read. The reader may end up working with information that is different from the current state.

### 5. Why Swing Is Not Thread-Safe

Swing components are generally not thread-safe. Swing uses an **Event Dispatch Thread (EDT)** to handle GUI-related operations.

If multiple threads directly modify GUI components, they can interfere with each other and produce inconsistent results.

Therefore, GUI applications generally follow this model:

```text
EDT → GUI events and UI updates
Worker Thread → Long-running/background tasks