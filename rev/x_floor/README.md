# X Floor

- **Category:** Reverse Engineering
- **Points:** 100
- **Status:** Attempted / Constraint Analysis

---

## 1. Challenge Overview

A mathematical reverse engineering challenge evaluating IEEE-754 floating-point operations, piecewise floor function step transformations, and nonlinear algebraic constraints.

## 2. Analysis & Constraints

1. **Floating-point Disassembly:** Utilized x87 / SSE instructions (`fld`, `fstp`, `cvttsd2si`, `roundsd`) to apply successive mathematical transformations:
   $$y_i = \lfloor a_i \cdot x_i^2 + b_i \cdot x_i + c_i \rfloor$$
2. **SMT Solver Modeling (Z3):** Formulated the discrete floor constraints into a system of bounded integer/real variables to solve for input coordinates $x_i$.
