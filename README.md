# Deterministic Spatial Engine
**DigiSim PS-1 – Udyam’26**

A digital hardware implementation that determines the **closest pair of 2-D Cartesian points** stored in memory.  
The system is built entirely using **digital logic components such as counters, registers, adders, multipliers, and comparators** and simulated in **Proteus**.

---

# Overview

This project implements a **digital circuit that calculates the distance between Cartesian coordinate pairs and determines the closest pair of points**.

The design demonstrates how a **mathematical algorithm can be translated into hardware** using fundamental digital components such as:

- Memory (EEPROM)
- Counters
- Registers
- Arithmetic circuits
- Comparators
- Control logic

The circuit automatically reads coordinate data from memory, compares distances between all possible pairs, and outputs the indices of the closest points.

---

# System Architecture

The complete design consists of the following main blocks:

- **EEPROM Memory Module**
- **Address Generation Counter**
- **Coordinate Registers**
- **Pair Generation Counters**
- **Distance Computation Unit**
- **Minimum Distance Comparator**
- **Tie-Breaking Metric Logic**
- **Display Interface**

These blocks work together to implement the algorithm entirely in hardware.

---

# Memory Organization

The coordinate values are stored inside an **EEPROM memory** in the form of a **HEX file**.

- The **first memory location stores the total number of coordinate points (n)**.
- Remaining memory locations store **x and y coordinates** of the points.

A **counter generates sequential memory addresses** at every clock pulse to automatically read the data.

---

# Register Initialization

The first memory value (n) is extracted and stored in a dedicated register called the **n-register**.

- The register is enabled **only once** when the counter output equals **zero**.
- After loading, the value of **n remains constant** throughout the computation.

---

# Pair Generation Logic

To compare all possible coordinate pairs, a **nested loop structure is implemented in hardware**.

Two counters are used:

- **i-Counter** → runs from **1 to n**
- **j-Counter** → runs from **i + 1 to n**

Comparators detect when the **j-counter reaches the limit**, after which:

1. `i` is incremented
2. `j` is reset to `i + 1`

This ensures **all combinations of points are checked without repetition**.

---

# Coordinate Extraction

The values of **i and j** are used to select corresponding coordinates from memory.

Memory addressing is organized such that:

- The **last three bits of the address represent the coordinate index**
- These bits are compared with counter outputs

When a match occurs, the corresponding coordinate values are stored in registers.

Four registers store:

```
xi
yi
xj
yj
```

Another address bit is used to distinguish between **x-coordinates and y-coordinates**, implemented using a **NOT gate**.

---

# Distance Computation

The squared distance between two points is calculated using the formula:

```
d² = (xi − xj)² + (yi − yj)²
```

This is implemented using:

- **Subtractor circuits**
- **Multipliers**
- **Adders**

The result is obtained as a **9-bit squared distance value**.

---

# Minimum Distance Detection

A register stores the **minimum distance found so far**.

- Initially loaded with the **maximum possible value**
- Each newly computed distance is compared with this value

If the new distance is **smaller**, then:

- The **minimum distance register is updated**
- The **corresponding indices (i, j) are stored**

---

# Tie-Breaking Metric

If two distances are equal, a **spatial metric** is used to break the tie.

The metric is defined as:

```
Metric = (xi × yi + xj × yj) mod (i × j)
```

The pair producing the **smaller metric value** is selected as the closest pair.

This ensures **deterministic decision making in hardware**.

---

# Output Display

Once the closest pair is determined:

- The **indices of the selected points are multiplied**
- The result is sent to a **BCD-to-7-segment display circuit**

The final output is displayed on a **seven-segment display**.

---

# Hardware Components Used

The system is implemented using basic digital IC components:

- Counters
- Registers
- Adders
- Subtractors
- Multipliers
- Comparators
- Multiplexers
- EEPROM memory
- Seven-segment display
- Control logic gates

---

# Tools Used

- **Proteus** – Digital circuit simulation
- **EEPROM HEX file generation**
- **Digital logic IC blocks**

---

# Key Outcomes

This project demonstrates:

- Implementation of a **mathematical algorithm using digital hardware**
- Design of **sequential control logic using counters**
- **Memory addressing and data extraction**
- **Hardware implementation of arithmetic operations**
- **Optimization of digital circuit architecture**
