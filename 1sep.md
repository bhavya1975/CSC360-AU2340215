# Comprehensive Class Reflection & Lecture Notes (01 September 2026)

## Overview of Core Topics Covered

1. **Linear Systems & Geometric Modeling: Defining a 2D Triangle via Linear Algebra**
2. **Abstract Data Types (ADTs): Stacks vs. Queues in Computation & System State Management**
3. **Hierarchical Data Structures: Foundations, Taxonomy, and Traversals of Trees**

---

## 1. Linear Systems & Geometric Modeling: The Mathematics of a Triangle

To bound a closed polygonal region such as a triangle in a 2-dimensional Cartesian plane ($\mathbb{R}^2$), we rely on systems of linear algebraic equations and linear inequalities.

### The Linear System Representation: $Ax = b$

A linear equation representing an infinite line in $\mathbb{R}^2$ is written in standard form as:

$$a_i x + b_i y = c_i$$

When framing a system of three intersecting lines that define the boundaries of a triangle, we express it compactly using matrix-vector notation:

$$egin{bmatrix} a_1 & b_1 \ a_2 & b_2 \ a_3 & b_3 \end{bmatrix} egin{bmatrix} x \ y \end{bmatrix} = egin{bmatrix} c_1 \ c_2 \ c_3 \end{bmatrix}$$

Or simply:

$$Ax = b$$

Where:
- $A \in \mathbb{R}^{3 	imes 2}$ is the coefficient matrix representing the normal vectors of the boundary lines.
- $x = egin{bmatrix} x & y \end{bmatrix}^T \in \mathbb{R}^2$ is the column vector of spatial coordinates.
- $b \in \mathbb{R}^3$ is the scalar constant vector representing line offsets.

```
       Line 1 (L1: a1*x + b1*y = c1)
                 \          /
                  \        /
                   \  V1  /
                    \    /
                     \  /
  Line 2 (L2) ------- V2 ------ V3 ------- (L2: a2*x + b2*y = c2)
                       \      /
                        \    /
                         \  /
              Line 3 (L3: a3*x + b3*y = c3)
```

### Degrees of Freedom and Boundary Determinacy

- **Underdetermined State ($< 3$ Lines):** Two non-parallel lines intersect at exactly one point ($A \in \mathbb{R}^{2 	imes 2}$). They divide the plane into four open, unbounded quadrants. Without a third constraining boundary, the closed triangular face cannot exist; there are infinitely many ways to complete the region.
- **Fully Determined Region ($3$ Boundary Lines):** Three distinct lines form a triangle if and only if:
    1. No two lines are parallel: $rac{a_1}{b_1}
       eq rac{a_2}{b_2}$, $rac{a_2}{b_2}
       eq rac{a_3}{b_3}$, and $rac{a_1}{b_1}
       eq rac{a_3}{b_3}$.
    2. The lines are non-concurrent (they do not all intersect at a single shared point, meaning $	ext{rank}([A \mid b]) = 3$).

### Coordinate Extraction: Pairwise Intersection Algorithm

To locate the three geometric vertices ($V_1, V_2, V_3$), solve the three independent $2 	imes 2$ sub-systems:

| Vertex | Line Intersection | Equation System to Solve | Resulting Coordinate |
| :--- | :--- | :--- | :--- |
| **$V_1$** | $L_1 \cap L_2$ | • $a_1 x + b_1 y = c_1$<br>• $a_2 x + b_2 y = c_2$ | $(x_1, y_1)$ |
| **$V_2$** | $L_2 \cap L_3$ | • $a_2 x + b_2 y = c_2$<br>• $a_3 x + b_3 y = c_3$ | $(x_2, y_2)$ |
| **$V_3$** | $L_3 \cap L_1$ | • $a_3 x + b_3 y = c_3$<br>• $a_1 x + b_1 y = c_1$ | $(x_3, y_3)$ |

Connecting $V_1
ightarrow V_2
ightarrow V_3
ightarrow V_1$ yields the polygonal perimeter. Replacing equality ($=$) with inequalities ($\le$ or $\ge$) defines the convex hull: the closed interior area of the triangle.

$$\mathcal{T} = \left\{ (x, y) \in \mathbb{R}^2 \;\middle|\; egin{aligned} a_1 x + b_1 y &\le c_1 \ a_2 x + b_2 y &\le c_2 \ a_3 x + b_3 y &\le c_3 \end{aligned}
ight\}$$

---

## 2. Linear Abstract Data Types: Stack vs. Queue

Stacks and Queues are sequential, constrained data structures governed by explicit rules for element insertion and removal.

### Comparative Feature Analysis

| Property | Stack | Queue |
| :--- | :--- | :--- |
| **Operational Discipline** | LIFO (Last-In, First-Out) | FIFO (First-In, First-Out) |
| **Access Points** | Single-ended: insertion and deletion occur at the **Top**. | Double-ended: insertion at **Rear/Tail**, removal at **Front/Head**. |
| **Primary Operations** | `push(item)`, `pop()`, `peek()` | `enqueue(item)`, `dequeue()`, `peek()` |
| **Algorithmic Complexity** | $O(1)$ amortized for push/pop | $O(1)$ for enqueue/dequeue |
| **Canonical Use Case** | Backtracking, function call stacks, syntax parsing. | Buffering, resource scheduling, multi-threaded pipelines. |

```
STACK (LIFO)                    QUEUE (FIFO)
+---+                           +---+---+---+---+
| C | <- Push / Pop (Top)   --> | C | B | A |   --> Dequeue (Front)
+---+                           +---+---+---+---+
| B |                           Enqueue (Rear)
+---+
| A |
+---+
```

### Concrete Execution Trace: The "Undo" ($	ext{Ctrl} + 	ext{Z}$) Pattern

Consider a text editor tracking user actions:
- **Action 1:** Type `"Hello"`
- **Action 2:** Type `" World"`
- **Action 3:** Apply **Bold** styling

#### Why Queues Fail for Ctrl + Z:
A Queue respects arrival order (FIFO). If an undo engine queried a Queue, it would pop the first operation performed:

$$	ext{Dequeue} \implies 	ext{Undo "Hello"}$$

This breaks user expectations: early baseline work is erased while leaving the most recent dependent operations orphaned.

#### Why Stacks Are Required:
A Stack stores historical snapshots by pushing each state onto the top of the runtime structure:

$$	ext{Stack}: [	ext{"Hello"}] \longrightarrow [	ext{"Hello"}, 	ext{" World"}] \longrightarrow [	ext{"Hello"}, 	ext{" World"}, 	ext{"Bold"} \, (	ext{Top})]$$

Triggering $	ext{Ctrl} + 	ext{Z}$ calls `pop()`, targeting the latest operation:

$$	ext{Pop} \implies 	ext{Undo "Bold"}$$

This preserves causal chronological coherence.

---

## 3. Non-Linear Hierarchical Data Structures: Trees

Trees break away from flat, linear execution paths, organizing records hierarchically through parent-child node relationships.

### Structural Anatomy & Terminology

- **Root:** The topmost node containing no parent (entry point).
- **Node:** An element containing data value and pointers to child nodes.
- **Edge:** The directed link establishing a parent-child connection.
- **Leaf (Terminal Node):** A node with degree 0 (no children).
- **Height of Tree:** The length of the longest path from root to a leaf node.
- **Depth of Node:** The number of edges from the root to that specific node.

```
                   [ Root: A ]            -- Depth 0
                   /                     [ B ]               [ C ]     -- Depth 1
           /     \                       [ D ]       [ E ]           [ F ]   -- Depth 2 (Leaves: D, E, F)
```

### Core Tree Taxonomy

1. **Binary Tree:** Every node has at most two children ($	ext{degree} \le 2$).
2. **Binary Search Tree (BST):** A binary tree with spatial ordering invariant:
   $$orall \, x \in 	ext{LeftSubtree}(Node), \, 	ext{val}(x) < 	ext{val}(Node)$$
   $$orall \, y \in 	ext{RightSubtree}(Node), \, 	ext{val}(y) > 	ext{val}(Node)$$
3. **Balanced Trees (AVL / Red-Black):** Self-balancing BSTs that guarantee height $H = O(\log N)$, preventing worst-case linear degeneration $O(N)$.
4. **B-Trees / B+ Trees:** N-ary self-balancing trees optimized for block storage, filesystem layouts, and database indexing.

### Systematic Traversal Strategies

Tree traversal algorithms systematically visit every node in a defined topological order.

#### 1. Depth-First Traversals (DFS)
DFS utilizes an implicit or explicit **Stack** to explore as far down a branch as possible before backtracking:

- **Pre-Order (Root $
  ightarrow$ Left $
  ightarrow$ Right):** Useful for cloning trees or evaluating prefix expressions.
- **In-Order (Left $
  ightarrow$ Root $
  ightarrow$ Right):** Produces elements in strictly sorted ascending order when executed on a BST.
- **Post-Order (Left $
  ightarrow$ Right $
  ightarrow$ Root):** Essential for bottom-up node deletion, memory deallocation, and postfix expression evaluation.

#### 2. Breadth-First Traversal (BFS / Level-Order)
BFS utilizes a **Queue** to explore nodes horizontal level-by-level:

- **Algorithm:** Enqueue root $
  ightarrow$ While Queue is non-empty: Dequeue node, process data, and Enqueue its left and right children.
- **Applications:** Finding shortest path on unweighted graphs, serialization, and peer-to-peer network broadcasting.

---

## 4. Summary & Algorithmic Paradigm Mapping

| Area / Concept | Underlying Mathematical / Algorithmic Paradigm | Primary Hardware / Runtime Application |
| :--- | :--- | :--- |
| **Linear Systems (Triangle)** | Vector Spaces, Matrix Elimination, Spatial Convex Hulls | Computer Graphics, Collision Detection, Finite Element Analysis |
| **Stacks (LIFO)** | Dynamic Sequential Memory, Depth-First Execution | Call Stack Execution, Expression Evaluation, Backtracking |
| **Queues (FIFO)** | Pipeline Queuing Theory, Breadth-First Processing | Task Scheduling, Network Packet Buffering, OS Process Management |
| **Trees (Hierarchical)** | Recursive Graph Substructures, Sub-linear Binary Search | Database Indexing (B+ Trees), Filesystem Hierarchies, AST Compilers |
