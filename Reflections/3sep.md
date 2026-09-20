# Reflection

## ASCII Tree

### Why is it important?

An ASCII tree represents a hierarchical structure using only text characters. This is useful because text-based interfaces are more universal and lightweight than graphical interfaces.

A GUI depends on graphical resources such as a display and window system, while a CLI mainly needs a terminal. This makes text especially useful for remote servers, cloud machines, containers, and systems where a GUI may not be available.

So, text/CLI is useful when we want **simplicity, reliability, remote access, and low resource usage**, while a GUI is better when we need a more visual and user-friendly experience.

---

## How do we draw a tree?

A terminal has a limited amount of space horizontally. If we keep putting nodes on the same line:

```text
Root  Child1  Child2  Child3  Child4  Child5  ...
```

the relationships between the nodes become difficult to understand.

Using multiple lines and indentation makes the hierarchy much clearer:

```text
Root
├── Child 1
├── Child 2
└── Child 3
```

For multiple levels:

```text
Root
├── A
│   ├── C
│   └── D
└── B
    ├── E
    └── F
```

Here:

- `├──` represents a child that has siblings after it.
- `└──` represents the last child.
- `│` shows that the branch continues.
- Spaces provide indentation for deeper levels.

The characters and their positions are therefore not just decoration. They communicate the **relationship and hierarchy between nodes**.

---

## Drawing vs Printing

When we draw a tree graphically, the system can use actual lines and shapes. When we print an ASCII tree, the computer is simply outputting characters.

Therefore, printing an ASCII tree means converting a hierarchical structure into a carefully arranged sequence of **characters, spaces, and line breaks**.

The underlying tree stays the same; only its representation changes.

### My Understanding

The main thing I understood is that **visualization does not always require graphics**. With the right use of indentation and characters, text can represent complex hierarchical structures clearly and work in environments where graphical interfaces are unavailable.
