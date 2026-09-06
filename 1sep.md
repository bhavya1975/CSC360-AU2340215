# Systems, Linear Structures, and Hierarchies: Architectural Lecture Notes
**Date:** September 01, 2026  
**Subject:** Advanced Computer Science & Mathematical Modeling

---

## Executive Overview

This technical reference document examines three foundational paradigms across computational mathematics and system architecture:

1. **Geometric Boundary Modeling:** Formalizing two-dimensional enclosed regions through systems of linear equations and half-space constraints.
2. **State Management Abstract Data Types:** Analyzing structural mechanics, temporal ordering, and application constraints in LIFO versus FIFO memory models.
3. **Hierarchical Topology & Tree Structures:** Exploring non-linear node graphs, balanced search properties, and traversal mechanics.

---

## 1. Mathematical Formalization of 2D Convex Regions

### Line Equations & System Matrix Formulation

In computational geometry and computer graphics, planar boundaries are constructed by intersecting half-spaces bounded by straight lines. An individual line $L_i$ in $\mathbb{R}^2$ is expressed in implicit scalar form as:

$$a_i x + b_i y = c_i$$

where $[a_i, b_i]^T$ represents the normal vector determining the line's spatial orientation, and $c_i$ denotes the offset scalar from the origin.

To enclose a 2-dimensional triangular domain, three concurrent line constraints must interact. Expressed in matrix notation:

$$\mathbf{A} \mathbf{x} = \mathbf{b}$$

$$\begin{bmatrix} a_1 & b_1 \\ a_2 & b_2 \\ a_3 & b_3 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} c_1 \\ c_2 \\ c_3 \end{bmatrix}$$

Here, $\mathbf{A} \in \mathbb{R}^{3 \times 2}$ maps the system coordinates $\mathbf{x} = [x, y]^T \in \mathbb{R}^2$ to the boundary offset vector $\mathbf{b} \in \mathbb{R}^3$.


---

## 2. Linear Memory Abstractions: Operational Mechanics & State Tracking

Linear abstract data types enforce constrained access patterns to maintain temporal consistency in dynamic application states.

### Comparison Matrix: Stacks vs. Queues

| Structural Dimension | Pushdown Stack | Processing Queue |
| :--- | :--- | :--- |
| **Access Invariants** | **LIFO** (Last-In, First-Out) | **FIFO** (First-In, First-Out) |
| **Interface Boundaries** | Single Access Vector (**Top**) | Dual Access Vectors (**Tail / Rear** for insertion, **Head / Front** for removal) |
| **Core Methods** | `push(v)`, `pop()`, `top()` / `peek()` | `enqueue(v)`, `dequeue()`, `front()` |
| **Time Complexity** | $O(1)$ constant time operations | $O(1)$ constant time operations |
| **Primary System Roles** | Frame evaluation, call stack, backtracking search, execution history. | Async message queues, process scheduling, buffer management. |

```
      STACK (LIFO Structure)               QUEUE (FIFO Pipeline)

         |   Elem C   |  <- Push / Pop      [Elem C] [Elem B] [Elem A]
         +------------+                       ^                 ^
         |   Elem B   |                       |                 |
         +------------+                    Enqueue           Dequeue
         |   Elem A   |                    (Tail)            (Head)
         +------------+
```

---

#### Flaw of Queue-Based State Recovery (FIFO):
If state transformations are queued sequentially, issuing a revert operation dequeues the *oldest* element ($e_1$):

$$\text{Dequeue}() \implies \text{Revert } e_1 \text{ ("Hello")}$$

*Outcome:* The baseline payload is destroyed while downstream modifications ($e_2, e_3$) remain applied onto invalid context.

#### Correctness of Stack-Based State Tracking (LIFO):
A stack preserves chronological dependency by unwinding state in exact inverse order of application:

$$\text{Stack State}: [e_1] \xrightarrow{\text{push}} [e_1, e_2] \xrightarrow{\text{push}} [e_1, e_2, e_3 \, (\text{Top})]$$

Triggering an undo command invokes `pop()`:

$$\text{Pop}() \implies \text{Revert } e_3 \text{ ("Bold")}$$

*Outcome:* The system steps backward along its causal timeline without corrupting foundational state.

---

## 3. Hierarchical Topologies: Tree Structures & Graph Search Algorithms

Unlike linear lists, tree topologies organize records across branching hierarchical layers, establishing clear parent-child node relationships.

```
                  ( [Node 0: Root] )             -- Height h = 2, Depth = 0
                    /            \
         ( [Node 1] )            ( [Node 2] )    -- Depth = 1
          /        \                 \
   ( [Leaf 3] )  ( [Leaf 4] )     ( [Leaf 5] )   -- Depth = 2 (Terminal Nodes)
```

### Core Terminology & Properties

* **Root Node:** Topmost ancestor with in-degree 0; serves as the canonical entry point.
* **Leaf Node:** Any terminal node with out-degree 0 (no child links).
* **Depth:** Distance measured in edges from the root to a specified target node.
* **Height:** Maximum edge path distance from a given node down to its furthest leaf descendant.
* **Branching Factor:** Maximum allowable children per internal node.

---

### Systematic Traversal Paradigms

Traversal patterns dictate how node data is visited and processed across non-linear memory spaces.

#### 1. Depth-First Search Patterns (DFS)
DFS relies on stack-based execution (recursive runtime stack or explicit data structure) to traverse deeply down individual branches before backtracking.

```
       ( A )              1. Pre-Order  (Root-Left-Right) : A -> B -> D -> E -> C -> F
      /     \             2. In-Order   (Left-Root-Right) : D -> B -> E -> A -> C -> F
    ( B )   ( C )         3. Post-Order (Left-Right-Root) : D -> E -> B -> F -> C -> A
    /   \      \
  (D)   (E)    (F)
```

* **Pre-Order (Root $\to$ Left $\to$ Right):** Processes current node prior to child branches; ideal for tree serialization, copying, and generating prefix expressions.
* **In-Order (Left $\to$ Root $\to$ Right):** Traverses the left branch, processes current node, then traverses the right branch. Executing In-Order on a BST extracts keys in sorted ascending order.
* **Post-Order (Left $\to$ Right $\to$ Root):** Evaluates child branches before processing parent nodes; optimal for memory cleanup, file system space calculation, and postfix evaluation.

#### 2. Breadth-First Search Pattern (BFS / Level-Order)
BFS explores tree nodes layer-by-layer horizontally using an auxiliary **Queue**.

* **Operational Mechanics:**
    1. Enqueue the root node into the processing queue.
    2. While queue is non-empty: Dequeue front node $u$, process $u$, and enqueue all immediate children of $u$ from left to right.
* **Primary Applications:** Finding shortest paths on unweighted graphs, level-by-level rendering, and network broadcast protocols.

---| Hierarchical Tree Traversal | Balanced Search Trees / B+ Trees | RDBMS Indexing (PostgreSQL/MySQL), File System Inodes |